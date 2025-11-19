12/11/25

- defining agentic ai
- five types of agentic ai
- components of agentic ai
- tools and frameworks for building agentic ai
- memory and context management
- MCP: how the agent connects
- Evaluating your agent
- use cases
- ethics for agents
- labs

### agentic ai is not the same as an ai agent

an agent is a single purpose entity handling a specific task

agentic ai is a goal driven system that collaborates across workflows devising their own strategies with minimal human insight

### defining agentic ai

an intelligent system designed to perceive its environment and make decisions and take action

the difference between generative ai and agentic ai is generative ai is a brainstormer and a content creator, agentic ai is the doer and decision maker

### evolution from scripts to agents

step 1, process automation - simple scripts executing a predefined workflow
step 2, supervised machine learning - feeding the ai hundreds of examples teaching it to learn and recognize patterns
step 3, generative ai - give it a prompt and it will generate something
step 4, agentic ai - give it a goal and it will formulate a plan and take action on its own

### five types of agentic ai
- instant rule follower - reacts now, no memory
- context keeper - keeps an internal state to handle partially observant situations, still uses rules but is informed by memory
- goal driven tool user - plans upcoming steps and calls tools
- decision optimizer - balances trade offs to maximize a score, chooses actions that maximize a utility score for the user
- self improving auto-pilot - improves models, rules, or policies from data/feedback

### putting it together: real world patterns

most agentic apps combine memory, goal driven tool use, a utility step to pick the best option, and a light learning loop from feedback

### components of agentic ai
- goal
- reasoning
- memory
- planning
- action

not necessarily in that order

### tools and frameworks for building agentic ai


LANGCHAIN is the main building block of ai applications (perhaps more research would be a good idea?)


### ethics for agentic ai's
- LLMS don't separate data from instructions, at their core they predict the next token; if text looks like a command they try to follow it
- prompt-injection risk. malicious instructions can be hidden inside documents/webpages/emails.
- the lethal trifecta - real danger emerges when three things are combined: exposure to outside content, access to private data, and the ability to communicate and share data with the outside world

what to do about it
- break the trifectas - don't give one workflow access to all three things listed in the lethal trifecta
- least privilege and narrow tools - restrict the models capability's when able
- harden inputs - filter/strip instructions from third party's 
- monitor and fail safe - log, rate limit, and be ready to disable misbehaving bots quickly


lmstudio.ai

