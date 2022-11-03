# roblox-gpt3-game
## Description
Create a simple Roblox game that demonstrate some capabiliies of GPT (GPT-3 now, and GPT-4 when available).

## Requirements
Game consists of
- one Player
- an NPC named Admiral that carries a conversation as if she were Admiral Grace Hopper
- an NPC named Stacker that retrieves and stacks blocks, and puts them away again.
- six block pads, each with its own color (red, orange, yellow, green, blue, purple)
- six blocks, each with its own corresponding color (same colors as pads)
- a base on which the blocks may be stacked on top of each other

The player may walk up to either of the NPCs and chat with them as follows:

### Chatting with the NPC named Admiral
When chatting with the NPC named Admiral, the NPC will respond as if she were Admiral Grace Hopper. For example, if the Player asks "When were you born", the Admiral would respond with something like "I was born on December 9, 1906." This will be implemented with a call to an OpenAI GPT model that includes the Player's question, receiving and displaying the response in the chat window.

Here is some [documentation on calling the OpenAI API](https://beta.openai.com/docs/api-reference/introduction)

#### GPT prompt and parameters
The GPT prompt for chatting with the NPC named Admiral will be something like this:
''The following is a conversation with Admiral Grace Hopper"

The GPT parameters will include something like this:
- Temperature: 0.9
- Maximum length: 150
- Stop sequences: "Human:", "Admiral:"
- Top P: 1
- Frequency penalty: 0
- Presence penalty: 0.6
- Best of: 1
- Inject start text: "↵Admiral"
- Inject restart text: "↵Human"

### Chatting with the NPC named Stacker
When chatting with the NPC named Stacker, the Player gives instructions to Stacker such as the following:
- Stack the blocks in rainbow color order
- Put the blocks away
- Stack the blocks whose colors appear on the Flag of Ukraine

The instruction will be sent to an OpenAI GPT model, which will respond with a series of actions for Stacker to perform. For example, an instruction to "Stack the blocks whose colors appear on the Flag of Ukraine" would result in the following actions to be returned and given to Stacker:
- Get the blue block
- Stack the blue block
- Get the yellow block
- Stack the yellow block

Stacker would implement these actions by visiting the corresponding game locations and picking/carrying/stacking blocks.

#### GPT prompt and parameters
The GPT prompt for chatting with the NPC named Stacker will be something like this:
''There is a red block, an orange block, a yellow block, a green block, a blue block, and a purple block. Perform the following actions step by step:

Command: Stack the blocks in their color's alphabetical order

Response: 
Get the blue block
Stack the blue block
Get the green block
Stack the green block
Get the orange block
Stack the orange block
Get the purple block
Stack the purple block
Get the red block
Stack the red block
Get the yellow block
Stack the yellow block

Command: Put the blocks away

Response: 
Remove the top block from the base
Place the block on the yellow pad
Remove the top block from the base
Place the block on the purple pad
Remove the top block from the base
Place the block on the orange pad
Remove the top block from the base
Place the block on the red pad
Remove the top block from the base
Place the block on the green pad
Remove the top block from the base
Place the block on the blue pad"

The GPT-3 parameters will include something like this:
- Temperature: 0
- Maximum length: 150
- Stop sequences: "Command:", "Response:"
- Top P: 0
- Frequency penalty: 0
- Presence penalty: 0
- Best of: 1
- Inject start text: "↵↵Response"
- Inject restart text: "↵↵Command"
