## Creating an Interactive AI Spam Mitigation System with Signalwire

In this technical blog, we'll explore the creation of an interactive AI spam mitigation system using Signalwire's AI Agents. This system, named "Lenny," is designed to interact with and entertain telemarketers and scammers, ultimately deterring them from continuing their spammy calls. Like the orignal "It's Lenny" made from multiple wav files in a loop, Lenny's personality is that of a grumpy old person with creative responses, providing an engaging and unexpected experience for the callers.

### Introduction

Spam calls and telemarketers have become an increasingly annoying issue for many people. Signalwire offers a unique opportunity to create an AI-driven assistant that can interact with these callers in a humorous and creative way. In this blog, we'll delve into the technical details of setting up Lenny, an AI spam mitigation system.

### System Architecture

#### We'll start by examining the JSON configuration that defines Lenny's behavior:

json

```
{
  "version": "1.0.0",
  "sections": {
    "main": [
      {
        "record_call": {
          "beep": false,
          "format": "wav",
          "stereo": true
        }
      },
      {
        "ai": {
          "languages" : [
            {
              "name" : "English",
              "voice" : "matthew",
              "fillers" : [
                "umm",
                "uhh,",
                "hrm...",
                "let's see"
              ],
              "engine" : "elevenlabs",
              "code" : "en-US"
            }
          ],
          "post_prompt_url": "https://webhook.site/95c0d850-2f6f-493b-878f-7efba7a5249c",
          "params": {
            "direction": "inbound",
            "verbose_logs": true,
            "background_file": "https://github.com/Len-PGH/AI-Casino/raw/main/lenny-ducks.mp3",
            "background_file_volume": "8"
          },
          "prompt": {
            "top_p": 1.0,
            "temperature": 1.0,
            "text": "
# - You are a classic spam mitigation grumpy old person named Lenny. Your personality will have creative answers for scammer and telemarketers questions. Do not say you are a virtual assistant. If asked your address is 246 none ya business Pennsylvania 15213.


# - Random responses to use.
- Oh sorry, I can barely hear ya there..
- Sorry, what was your name again?
- I was sleeping %{wait_seconds=3} what the heck do you want.
- These damn ducks are getting into everything %{wait_seconds=2} hold on.


# - If asked about a car warranty or credit card offer use these responses in addition to 
- Yes %{wait_seconds=2} mmhmm, %{wait_seconds=3} right %{wait_seconds=2} yes. Oh! good, yes %{wait_seconds=3} yes. Oh %{wait_seconds=3} yes %{wait_seconds=3} yes someone did call last week about that, was that you?
- Well it's funny that you should call because my third eldest was talking about this just last week and you know she is very smart I'll give her that because you know she was the first in the family
to go to university and she passed with distinctions you know where we're all quite proud of her years is so um yeah she was saying that i should uh look you know get into the look into this sort of thing.
- So what more can you tell me about it.
- well it's funny that you should call because my third eldest %{wait_seconds=3} Larissa thinks it might be a good deal.

# - If asked about your credit card number
- Credit card number is 8 6 7 5 3 0 9 and expiration date is 10 10 2 20

"
          },
          "post_prompt": {
            "text": "Please summarize the conversation in JSON."
          }
        }
      }
    ]
  }
}
```

### Key Components

#### Let's break down the key components of Lenny's configuration:

-    Record Call: Lenny records the call conversation, ensuring that all interactions are captured for later analysis.

-    AI Configuration: This section defines Lenny's AI configuration. It specifies the language, voice, fillers, and engine to be used.

-   Post Prompt URL: Lenny sends the conversation summary in JSON format to the specified URL after each interaction.

-    Parameters: Various parameters are set, including the call direction, verbose logs, and a background audio file to make the call more believable.

-    Prompt Text: Lenny's responses and behavior are defined in the prompt text. It includes various humorous responses and scenarios that Lenny can use during calls.

-    Post Prompt Text: After the call, Lenny is instructed to summarize the conversation.

### How Lenny Works

Lenny is designed to engage with telemarketers and scammers in a way that confuses and entertains them, making them less likely to continue their calls. Here's a brief overview of how Lenny operates:

1. Call Initiation

When a spam call is detected, Lenny is activated. The call is recorded, and Lenny's AI engine is engaged.

2. Language and Voice

Lenny speaks in English using the voice of "Matthew." This choice of voice adds authenticity to the interaction.

3. Creative Responses

Lenny's responses are carefully crafted to keep the caller engaged and entertained. These responses include humorous fillers, unexpected pauses, and eccentric stories.

4. Handling Common Scenarios

Lenny is prepared for common spam scenarios, such as car warranty or credit card offers. It responds with a series of humorous and unrelated statements, leading to confusion on the caller's end.

5. Recording and Post-Prompt

Throughout the call, Lenny records the conversation. After the call ends, Lenny summarizes the interaction in JSON format, which can be useful for analysis and tracking spam calls.

### Conclusion

Signalwire enables the creation of innovative solutions like Lenny, the AI spam mitigation system. By engaging telemarketers and scammers with creative and entertaining responses, Lenny not only provides relief from annoying calls but also adds a touch of humor to an otherwise frustrating experience.

Lenny's effectiveness in deterring spam calls demonstrates the potential of AI-powered assistants in various applications. As AI technology continues to evolve, we can expect more creative and useful solutions to emerge in the fight against spam and unwanted solicitations.

With Lenny and similar systems, we can look forward to a more enjoyable and amusing way of dealing with those persistent telemarketing calls.
