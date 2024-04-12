<style type='text/css'>
div.embeddedServiceHelpButton div.helpButton button.uiButton:focus,
div.modalContainer.embeddedServiceSidebar button.minimizedContainer.embeddedServiceSidebarMinimizedDefaultUI:focus {
    outline: 3px solid #ffffff!important;
}

.showDockableContainer header.sidebarHeader button.minimizeButton:focus,
.showDockableContainer header.sidebarHeader button.minimizeButton:focus {
outline: 2px auto #ffffff;
}
	.embeddedServiceHelpButton .helpButton .uiButton {
		background-color: #008375;
		font-family: "Arial", sans-serif;
	}
	.embeddedServiceHelpButton .helpButton .uiButton:focus {
		outline: 1px solid #008375;
	}
</style>

<script type='text/javascript' src='https://service.force.com/embeddedservice/5.0/esw.min.js'></script>
<script type='text/javascript'>
	var initESW = function(gslbBaseURL) {
		embedded_svc.settings.displayHelpButton = true; //Or false
		embedded_svc.settings.language = ''; //For example, enter 'en' or 'en-US'

		embedded_svc.settings.defaultMinimizedText = 'Chat with Sales'; //(Defaults to Chat with an Expert)
		//embedded_svc.settings.disabledMinimizedText = '...'; //(Defaults to Agent Offline)

		//embedded_svc.settings.loadingText = ''; //(Defaults to Loading)
		//embedded_svc.settings.storageDomain = 'yourdomain.com'; //(Sets the domain for your deployment so that visitors can navigate subdomains during a chat session)

		// Settings for Chat
		//embedded_svc.settings.directToButtonRouting = function(prechatFormData) {
			// Dynamically changes the button ID based on what the visitor enters in the pre-chat form.
			// Returns a valid button ID.
		//};
		//embedded_svc.settings.prepopulatedPrechatFields = {}; //Sets the auto-population of pre-chat form fields
		//embedded_svc.settings.fallbackRouting = []; //An array of button IDs, user IDs, or userId_buttonId
		//embedded_svc.settings.offlineSupportMinimizedText = '...'; //(Defaults to Contact Us)
//Code to facilitate retrieving associated cookies from the user browser and storing it as Coupon Code in LiveChatTranscript		
//Retrieve all cookies

var x = document.cookie;
var cookieValue='';
var foundInsession =false;
    console.log(x); //log all cookies
    
	//Split cookies and process each one	 
	
	x.split(';').forEach(function(el) {
     		var y = el.split('=');
		if(foundInsession) return;
		     console.log(y);
		     console.log(y[1]);
		
//Extract values for specific cookies
// First the code checks for cookieValue in 'wex_cc_session' and if empty it then checks in 'wex_cc_persistent'.
   
	 	if( y[0].trim()==='wex_cc_session' ){
		       	if(y[1]){
		     		 cookieValue = y[1].split('|')[0];
				foundInsession = true;
				return;
	  			
		       	}
      
      		}
		if(y[0].trim()==='wex_cc_persistent') {
 		if(y[1]){
     		 	cookieValue = y[1].split('|')[0];
      		 }
		}
 	  	
    		console.log(cookieValue);//log extracted cookieValue
	});
 	
   
//  Array to include pre-chat fields and map it to the associated LiveChatTranscript fields.
		
		embedded_svc.settings.extraPrechatFormDetails = [{
  		"label": "Coupon Code",
  		"value": cookieValue,
  		"displayToAgent": true,
  		"transcriptFields" : ["Coupon_Code__c"]
		},{
		  "label":"First Name",  
		  "transcriptFields": ["FirstName__c"]
		},{
		  "label":"Last Name", 
		  "transcriptFields": ["LastName__c"]
		},{
		  "label":"Email", 
		  "transcriptFields": ["Email__c"]
		},{
		  "label":"Company", 
		  "transcriptFields": ["Company__c"]
		},{
		  "label":"Phone", 
		  "transcriptFields": ["Phone__c"]
		}];
		embedded_svc.settings.enabledFeatures = ['LiveAgent'];
		embedded_svc.settings.entryFeature = 'LiveAgent';

		embedded_svc.init(
			'https://wexinc--stagefull.sandbox.my.salesforce.com',
			'https://wexinc--stagefull.sandbox.my.salesforce-sites.com/chat',
			gslbBaseURL,
			'00DU8000000Tosf',
			'Wex_Inc_Bot_Team',
			{
				baseLiveAgentContentURL: 'https://c.la2s-core2.sfdc-lywfpd.salesforceliveagent.com/content',
				deploymentId: '572U80000008ofZ',
				buttonId: '573U80000002GlR',
				baseLiveAgentURL: 'https://d.la2s-core2.sfdc-lywfpd.salesforceliveagent.com/chat',
				eswLiveAgentDevName: 'EmbeddedServiceLiveAgent_Parent04IU8000000RnMPMA0_18e3837c6b5',
				isOfflineSupportEnabled: false
			}
		);
	};

	if (!window.embedded_svc) {
		var s = document.createElement('script');
		s.setAttribute('src', 'https://wexinc--stagefull.sandbox.my.salesforce.com/embeddedservice/5.0/esw.min.js');
		s.onload = function() {
			initESW(null);
		};
		document.body.appendChild(s);
	} else {
		initESW('https://service.force.com');
	}
</script>
