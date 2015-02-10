Flow.Login
==================================================================================================================================================================

A TYPO3 Flow package that manages accounts and login authentication.

This tool is a lightweight single purpose authentication wrapper around a given package.
The package is built on the features that are provided in the security framework of TYPO3.Flow and require only a little configuration.

Usage:
- Security layer for any application
- Inspiration

Authentication setup
--------------------

The initial view will show a login box.

When authenticated but not configured, the package will redirect to the signedInAction by default.
The signedIn view will show you with what "account.identifier" you have been authenticated.

Through Settings.yaml you will be able to configure options like redirects to a package, open registration for anonymous users
and so on.

Quickstart
----------

!!Important!! Yes, you will need a tool to create an account for you, i'd refer you to [UserManagement](https://github.com/svparijs/TYPO3.UserManagement) [Work in Progress]
This section will get you up and running.

#####Routing

To be able to address the login feature you will need to add these routes in the general Configuration/Routes.yaml

	-
	  name: 'Login'
	  uriPattern: '<LoginSubroutes>'
	  subRoutes:
	    LoginSubroutes:
	      package: Flow.Login

Login Panel
-----------

* Pre-requirements

- jQuery
- jQuery Form
- Bootstrap 3

You need to add these pre-requirements to your website in order to have a modal login.

The javascript that will handle your Action calls.

	<script src="{f:uri.resource(path: 'JavaScript/Login.js', package: 'Flow.Login')}"></script>

The link that will trigger the login panel:

	<a class="login-panel" data-toggle="modal" data-target="#modal-login" href="{f:uri.action(controller:'Login', action: 'loginPanel', package: 'Flow.Login')}">Login Action</a>

The modal that will be displayed:

	<div class="modal hide fade" id="modal-login">
    </div>

Account ViewHelper
------------------

Add the viewhelper to fluid and call the viewhelper function.

	{namespace secure=Flow\Login\ViewHelpers}

	<secure:account propertyPath="party.name" />

Redirect to Login page
----------------------

When the action is unauthorized the TYPO3.Flow framework will redirect the package to a location set with the Settings.yaml configuration.

	TYPO3:
	  Flow:
	    security:
	      authentication:
	        providers:
	          DefaultProvider:
	            entryPoint: 'WebRedirect'
	            entryPointOptions:
	              routeValues:
                    '@package': 'Flow.Login'
                    '@controller': 'Login'
                    '@action': 'index'

See for reference: http://flow.typo3.org/documentation/guide/partiii/security.html
