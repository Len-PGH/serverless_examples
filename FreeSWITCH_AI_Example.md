

# LenAI Bot

Want to add an AI Agent to your FreeSWITCH instance?  Here we have a FreeSWITCH dialplan example bridging to a Signalwire AI Agent. This is a twist of the classic "It's Lenny" spam call mitigation with Signalwire's new AI Agent Capabilities.

### FreeSWITCH Dialplan

```xml
 <extension name="testing_ai" continue="false" uuid="6d0ecaef-9049-4920-8d1a-fc97ff4731f0">
	<condition field="destination_number" expression="^55555$">
		<action application="ring_ready" data=""/>
		<action application="answer" data=""/>
		<action application="sleep" data="500"/>
		<action application="set" data="hangup_after_bridge=true"/>
		<action application="set" data="ringback=local_stream://default"/>
		<action application="bridge" data="sofia/external/FreeSWITCH_AI@dev-freeswitch-ai.dapp.swire.io;transport=tcp"/>
	</condition>
</extension>
```

* ***In the bridge be sure to replace `FreeSWITCH_AI@dev-freeswitch-ai.dapp.swire.io` with your Domain App sip address***



##

# FreeSWITCH Dialplan Details

The given dialplan defines an extension within a FreeSWITCH configuration file. Let's break down its components for a clearer understanding:

## Extension

```xml
<extension name="testing_ai" continue="false" uuid="6d0ecaef-9049-4920-8d1a-fc97ff4731f0">
```
 -   name="testing_ai": The name of the extension. This is a unique identifier for the extension.
 -   continue="false": Indicates whether FreeSWITCH should continue processing more extensions if this extension is executed. false means no further extensions will be processed.
 -   uuid="6d0ecaef-9049-4920-8d1a-fc97ff4731f0": A unique identifier for this specific extension instance.


## Condition

```xml
<condition field="destination_number" expression="^55555$">
```

- field="destination_number": This specifies that the condition is based on the destination number of the call.
    expression="^55555$": A regular expression that matches the number 55555. Only calls to this exact number will trigger the actions defined in this extension.

## Actions

The actions are executed sequentially when the condition is met:

## Ring Ready

```xml

<action application="ring_ready" data=""/>
```
-   Sends a ringing signal to the caller, indicating that the call is being processed but not yet answered.

## Answer

```xml

<action application="answer" data=""/>
```

-   Answers the call.

## Sleep

```xml

<action application="sleep" data="500"/>
```

-   Pauses the call processing for 500 milliseconds.

## Set hangup_after_bridge

```xml

<action application="set" data="hangup_after_bridge=true"/>
```

-   Sets a variable `hangup_after_bridge` to true, which means the call will be hung up immediately after the bridge application completes its execution.

## Set Ringback Tone

```xml
<action application="set" data="ringback=local_stream://default"/>
```

-  Sets the ringback tone to be played to the caller. In this case, it uses a default local stream.

## Bridge

```xml

    <action application="bridge" data="sofia/external/FreeSWITCH_AI@dev-freeswitch-ai.dapp.swire.io;transport=tcp"/>
```

- Bridges the call to the SIP URI FreeSWITCH_AI@dev-freeswitch-ai.dapp.swire.io using the TCP transport. This effectively forwards the call to the specified SIP address.




Each `<action>` element represents a step in the call handling process. This configuration is particularly useful for setting up specialized call routing and handling behaviors in FreeSWITCH.

This block provides a detailed breakdown of the extension, condition, and actions within the provided FreeSWITCH dialplan configuration.
