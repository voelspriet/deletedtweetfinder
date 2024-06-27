<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Deleted Tweet Finder</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        .logo-img {
            max-width: 100px;
            max-height: 100px;
        }
        @media (min-width: 768px) {
            .logo-img {
                max-width: 200px;
                max-height: 200px;
            }
        }
        .donate-button {
            background-color: #0070ba;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 20px;
            font-weight: bold;
            transition: background-color 0.3s ease;
        }
        .donate-button:hover {
            background-color: #005ea6;
        }
        .manual-check-notice {
            background-color: #fff3cd;
            border: 1px solid #ffeeba;
            border-radius: 4px;
            padding: 10px;
            margin-top: 10px;
            font-style: italic;
        }
        #bingInstructions {
            display: none;
            margin-top: 10px;
            padding: 10px;
            background-color: #f8f9fa;
            border: 1px solid #dee2e6;
            border-radius: 4px;
        }
        #compositeResults {
            margin-top: 20px;
        }
        .service-result {
            margin-bottom: 10px;
            padding: 10px;
            border: 1px solid #dee2e6;
            border-radius: 4px;
        }
        #serviceExplanation {
            margin-top: 10px;
            padding: 10px;
            background-color: #f8f9fa;
            border: 1px solid #dee2e6;
            border-radius: 4px;
        }
        .service-status {
            display: inline-block;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            margin-right: 5px;
        }
        .status-up { background-color: green; }
        .status-down { background-color: red; }
        .status-slow { background-color: orange; }
        .status-unknown { background-color: #6c757d; }
        
        .share-buttons {
            margin-top: 10px;
        }
        .share-buttons button {
            margin-right: 5px;
            background-color: #f8f9fa;
            border: 1px solid #dee2e6;
            color: #495057;
        }
        .share-buttons button:hover {
            background-color: #e9ecef;
        }
        
        .tutorial-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.7);
            z-index: 1000;
            display: none;
        }
        .tutorial-content {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            padding: 20px;
            border-radius: 5px;
            max-width: 80%;
        }
        .tutorial-step {
            display: none;
        }
        .tutorial-step.active {
            display: block;
        }
    </style>
</head>
<body>
    <div class="container my-4">
        <div class="row align-items-center">
            <div class="col-md-4 text-center text-md-start mb-3 mb-md-0">
                <img src="ja.jpeg" alt="Deleted Tweet Finder Logo" class="logo-img">
            </div>
            <div class="col-md-8">
                <h1 class="text-center text-md-start">Deleted Tweet Finder V2.3</h1>
                <p class="lead text-center text-md-start">Search for deleted tweets across multiple archival services.</p>
                <p class="text-center text-md-start"><a href="https://www.digitaldigging.org/p/deleted-tweet-finder-tool" target="_blank">What this tool does</a></p>
            </div>
        </div>

        <form class="mt-4" onsubmit="return redirectToService()">
            <div class="row g-3">
                <div class="col-md-6">
                    <label for="urlInput" class="form-label">Enter URL:</label>
                    <input type="text" class="form-control" id="urlInput" name="urlInput" value="https://twitter.com/jack" required>
                </div>
                <div class="col-md-4">
                    <label for="serviceSelect" class="form-label">Choose Service:</label>
                    <select class="form-select" id="serviceSelect" name="serviceSelect" onchange="updatePlaceholder(); toggleServiceInstructions(); showServiceExplanation(); clearCompositeResults();">
                        <option value="google">Google Cache</option>
                        <option value="wayback">Wayback Machine</option>
                        <option value="archive">Archive.is</option>
                        <option value="ghostarchive">Ghost Archive</option>
                        <option value="usersearch">User Search</option>
                        <option disabled>──────────</option>
                        <option value="bing">Bing Search (Manual Check)</option>
                        <option value="yandex">Yandex Search (Manual Check)</option>
                        <option value="baidu">Baidu Search (Manual Check)</option>
                        <option disabled>──────────</option>
                        <option value="composite">Composite Search</option>
                        <option value="openall">Open All</option>
                    </select>
                </div>
                <div class="col-md-2 d-flex align-items-end">
                    <button type="submit" class="btn btn-primary w-100">Go</button>
                </div>
            </div>
        </form>

        <div id="serviceExplanation" style="display: none;"></div>

        <div id="serviceInstructions" class="mt-3" style="display: none;"></div>

        <div id="manualCheckNotice" class="manual-check-notice mt-3" style="display: none;">
            <strong>Note:</strong> This search engine requires manual checking for cached pages
