Rule Machine

Rule Machine is a generalized rule engine for SmartThings.  It allows you to predicate actions to be taken in SmartThings by a logical rule based on specified conditions of your system.

What are rules?

A rule is a method of specifying certain conditions and their truth relationships in order to cause some action to take place in SmartThings.  For example, one person posed this case:

Suppose my presence or my wife’s presence is home, there is motion in the bedroom, it’s between 8 PM and 11 PM, and the temperature is below 65 — if those conditions are met, turn on the electric blanket.

In order for this action to take place in SmartThings based on those conditions, a SmartApp will need to evaluate those conditions, and if they are met, cause the action.  Rule Machine is a SmartApp that allows you to specify the conditions, and the rule they must meet, and the desired action to take place.

What are conditions?

Rule Machine allows a wide range of possible conditions to be specified.  In particular, the following capabilities in a SmartThings system can be tested.  Each condition is one such test.  The supported capabilities and states are the following:

	Acceleration	active / inactive
	Contact	open / closed
	Days of week	[Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday]
	Humidity	=     !=    <    >    <=   >=  relative to a number
	Illuminance	=     !=    <    >    <=   >=  relative to a number
	Lock	locked / unlocked
	Mode	[ any of your location’s modes ]
	Motion	active / inactive
	Presence	present / not present
	Switch	on / off
	Temperature	=     !=    <    >    <=   >=  relative to a number
	Time of day	between two times, including sunrise / sunset with offsets

For each capability, one or more devices can be selected, and the device state required for the condition to be met is selected.  When multiple devices are selected, the condition may apply for ANY (default)  or ALL of the devices.  For example, the conditions for the electric blanket case are,
	my presence or my wife’s presence is present (Any)
	bedroom motion is active
	time of day is between 8:00 PM and 11:00 PM
	bedroom temperature is <  65
How is a rule defined?

A rule is a logical expression built up using the conditions and the two logical operators AND and OR.  A logical expression defines the logical relationship between the various conditions, in order to decide if the end action should be taken or not, by evaluating the truth of the defined rule.  In the electric blanket case, we have a very simple rule:

	my presence or my wife’s presence is present AND
	bedroom motion is active AND
	time of day is between 8:00 PM and 11:00 PM AND
	bedroom temperature is <  65

There can be more complex rules that this.  Suppose we want the same basic rule, but want it to apply if either bedroom motion is active or the bedroom door is closed.  We would add the additional condition of “bedroom door closed”.  That rule would be this:

	my presence or my wife’s presence is present AND
	(bedroom motion is active OR bedroom door is closed) AND
	time of day is between 8:00 PM and 11:00 PM AND
	bedroom temperature is <  65

In this example, we have used parentheses to group two conditions into a sub-rule: (bedroom motion is active OR bedroom door is closed).  Rule Machine allows arbitrarily complex rules to be defined, with parentheses used to group conditions into sub-rules.  It allows sub-rules to any level, and it allows any number of conditions.  

Rule Machine is a fully generalized rules engine. 

Rule Evaluation and Actions

Once Rule Machine is installed with conditions and rule, what happens next?  Whenever something happens in SmartThings that could affect the rule, Rule Machine evaluates the rule to see if it is true or false.  If it becomes true, then it will take some action.  In the case of the electric blanket, the rule would be evaluated whenever any of the following things happen:

	the state of my presence or my wife’s presence changes
	the bedroom motion goes active or inactive
	the bedroom door is opened or closed
	the time becomes 8:00 PM, or becomes 11:00 PM
	the bedroom temperature is reported

Since our rule for this case involves all of these possible events, any of those events might be the one that changes the evaluation outcome from false to true.  If that happens, Rule Machine will turn on the electric blanket.

When Rule Machine evaluates the state and determines the rule to have become true, two optional actions to be taken have been selected during installation:  The app can run a Routine, and / or the app can turn on some switches.  When Rule Machine determines the rule to have become false, it can run a Routine and / or turn off some switches.

The reason for only these two choices for actions to take upon rule evaluation is that it is not the intent of Rule Machine to have an elaborate action capability.  Elaborate actions can be done by so many different SmartApps, that there would be no point in attempting to replicate all of that functionality.  Instead, Rule Machine provides the two most likely means of launching some other action: running a Routine or flipping a switch.  The latter could be a virtual switch, tied into other automations, including Smart Lighting.  So Rule Machine is the rule engine front end, and links into other apps for backend actions.  Often, either running a Routine or flipping a switch is all the action that is needed, as is the case with the electric blanket example.

This is a preliminary release of Rule Machine.  Additional capabilities for conditions could be defined, if a need is shown.  While it has been tested extensively, it is not possible to test the infinite combinations of conditions and rules, so it is quite possible that there are latent bugs.  Please report these should you encounter one.



