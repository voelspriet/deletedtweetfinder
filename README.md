Deleted Tweet Finder

Overview

The Deleted Tweet Finder is a web application designed to help users locate archived versions of deleted tweets using various archival services. It offers a user-friendly interface to input tweet URLs and select archival services for searching the deleted content.

Features

	•	Multiple Archival Services: Supports Google Cache, Wayback Machine, Archive.is, Ghost Archive, User Search, Bing Search, Yandex Search, Baidu Search, Composite Search, and Open All options.
	•	Service Explanations: Provides detailed explanations for each archival service.
	•	Manual Check Notices: Displays instructions for services requiring manual checks.
	•	Composite Search: Aggregates results from all supported services.
	•	Share Buttons: Allows users to share search results on social media or via email.
	•	Service Status Check: Indicates the operational status of each service.
	•	Interactive Tutorial: Guides users through the steps to use the application.

 Head Section

The <head> section includes meta-information, external stylesheets, and custom CSS for styling the application.
<head>
    <!-- Meta Information -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Deleted Tweet Finder</title>

    <!-- External Stylesheets -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">

    <!-- Internal Stylesheet -->
    <style>
        <!-- Custom CSS Rules -->
    </style>
</head>

Body Section

The <body> section contains the main content and functionality of the application.


Logo and Header

Displays the application logo and header information.

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


Search Form

Provides a form for users to input a tweet URL and select an archival service.

<form class="mt-4" onsubmit="return redirectToService()">
    <div class="row g-3">
        <div class="col-md-6">
            <label for="urlInput" class="form-label">Enter URL:</label>
            <input type="text" class="form-control" id="urlInput" name="urlInput" value="https://twitter.com/jack" required>
        </div>
        <div class="col-md-4">
            <label for="serviceSelect" class="form-label">Choose Service:</label>
            <select class="form-select" id="serviceSelect" name="serviceSelect" onchange="updatePlaceholder(); toggleServiceInstructions(); showServiceExplanation(); clearCompositeResults();">
                <!-- Options for various services -->
            </select>
        </div>
        <div class="col-md-2 d-flex align-items-end">
            <button type="submit" class="btn btn-primary w-100">Go</button>
        </div>
    </div>
</form>

Service Explanation and Instructions

Displays explanations and instructions based on the selected archival service.

<div id="serviceExplanation" style="display: none;"></div>
<div id="serviceInstructions" class="mt-3" style="display: none;"></div>
<div id="manualCheckNotice" class="manual-check-notice mt-3" style="display: none;">
    <strong>Note:</strong> This search engine requires manual checking for cached pages.
</div>

Bing Instructions

Provides specific instructions for using Bing to access cached pages.

<div id="bingInstructions" class="mt-3">
    <h5>How to access the cached page using Bing:</h5>
    <ol>
        <li>After clicking "Go", a new tab will open with Bing search results for the URL you entered.</li>
        <li>Look for the search result that matches the URL you're looking for.</li>
        <li>Next to the URL in the search result, you'll see a small downward-pointing arrow. Click on this arrow.</li>
        <li>In the dropdown menu that appears, click on "Cached".</li>
        <li>This will open the most recent cached version of the page that Bing has stored.</li>
    </ol>
    <p>Note: If you don't see a "Cached" option, it means Bing doesn't have a cached version of that page available.</p>
</div>

Service Status

Indicates the operational status of each archival service.

<div class="row mt-3">
    <div class="col-12">
        <h5>Service Status:</h5>
        <div id="serviceStatus"></div>
    </div>
</div>

Composite Results and Share Buttons

Displays composite search results and provides buttons to share the results. (Not finished yet)

<div id="compositeResults"></div>
<div class="share-buttons text-center mt-3">
    <button class="btn btn-sm" onclick="shareResults('twitter')"><i class="fab fa-twitter"></i> Twitter</button>
    <button class="btn btn-sm" onclick="shareResults('facebook')"><i class="fab fa-facebook-f"></i> Facebook</button>
    <button class="btn btn-sm" onclick="shareResults('email')"><i class="fas fa-envelope"></i> Email</button>
</div>

Spinner and Tutorial Reset

Displays a loading spinner during searches and a button to reset the tutorial.

<div class="text-center mt-3">
    <div class="spinner-border text-primary d-none" id="spinner" role="status">
        <span class="visually-hidden">Loading...</span>
    </div>
</div>
<div class="text-center mt-3">
    <button class="btn btn-secondary" onclick="resetTutorial()">Reset Tutorial</button>
</div>


Donation and Footer

Includes a PayPal donation button and footer information.

<div class="text-center mt-5">
    <form action="https://www.paypal.com/donate" method="post" target="_top">
        <input type="hidden" name="hosted_button_id" value="9P7DAQ96M5FW4" />
        <input type="submit" class="donate-button" value="Donate via PayPal" />
    </form>
</div>
<footer class="text-center mt-5">
    &copy; 2024 Henk van Ess | <a href="https://digitaldigging.org" target="_blank">digitaldigging.org</a><br>
    Proudly Made with the help of Claude Sonnet
</footer>

Tutorial Overlay

An overlay that guides users through the steps to use the application.

<div class="tutorial-overlay" id="tutorialOverlay">
    <div class="tutorial-content">
        <div class="tutorial-step active" data-step="1">
            <h3>Welcome to Deleted Tweet Finder!</h3>
            <p>This tool helps you find archived versions of deleted tweets. Let's get started!</p>
            <button class="btn btn-primary" onclick="nextTutorialStep()">Next</button>
        </div>
        <!-- Additional tutorial steps -->
    </div>
</div>


JavaScript Functions

	•	updatePlaceholder: Updates the placeholder URL based on the selected service.
	•	redirectToService: Handles the form submission and redirects to the appropriate archival service.
	•	isValidURL: Validates the input URL.
	•	toggleServiceInstructions: Displays specific instructions for manual checking services.
	•	showServiceExplanation: Displays explanations for the selected service.
	•	clearCompositeResults: Clears previous composite search results.
	•	performCompositeSearch: Performs a composite search and displays results.
	•	updateServiceStatus: Checks and displays the status of each archival service.
	•	shareResults: Shares the search results on social media or via email.
	•	showTutorial, nextTutorialStep, closeTutorial, resetTutorial: Manages the tutorial overlay.


External Scripts

	•	Bootstrap JavaScript Bundle: Provides interactivity and component behavior.

 <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js"></script>

 Usage

	1.	Enter URL: Input the URL of the tweet you want to find.
	2.	Choose Service: Select the archival service from the dropdown menu.
	3.	Search: Click the "Go" button to perform the search.
	4.	Review Results: Follow the instructions for manual check services or view composite results.
	5.	Share: Use the share buttons to share the search results.
	6.	Donate: Support the project via PayPal.

 Feel free to customize
