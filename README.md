The system must be structured as a classic agent loop: **Perceive -> Think -> Act -> Repeat**
***Modules to be developed:***
- **[[Perception Module]] `(perception.py)` -** Most critical component, directly in charge of the LLM's performance. This script's sole responsibility is to capture the current browser's state, simplify it, and convert it to a easy to understand format for the LLM.
- **Action Module `(action.py)` -** A dedicated module which translates the model's (`inference.py`) structured output into actual Playwright API calls. **Necessary, separates the model's logic from the execution engine, dramatically increasing output performance.**
- **[[Inference Module ]]`(inference.py)` -** Hosts the fine-tuned model. Receives state representation and user intent, outputting a structured action.
- **Session Management `(session_manager.py)` -** A single, robust module for managing browser contexts, state, and stealth configurations.
- **Agent Core `(agent.py)` -** Takes in user intent, queries `perception.py` for current browser state, pass to `inference.py`, and commands `action.py` to execute the returned command
## User Intent
The prompt for the LLM (`inference.py`) will not be just a state. It must consist of the **user's goal** and the **current state**.
- **Example:** `{"goal": "Login to Github with the username 'test'", "dom_tree": {}`
## Action Space
The model must not generate raw Playwright code. This invites syntax errors. Instead, define a structured action space. The LLM's task is to output a JSON object representing a specific action.

**Example Commands:**
- CLICK(id)
- TYPE(id, text)
- SELECT(id, value)
- SCROLL(direction, amount)
- FINISH(status, message)

**Example LLM (`inference.py`) Output:** 
`{"command": "TYPE", "target_id": "login_field_12", "text": "test"}`

The `action.py` module will then be responsible for parsing this JSON and executing `page.locator('[data-untamed-id="login_field_12"]').type('testuser')`.

## Training Strategy
We must create a **[[scalable data generation pipeline]]** in order to expect the fine-tuning to yield meaningful results

## Benchmarking
**Benchmark Suite:** Use our canonical tasks as a standardized benchmark.
**Key Metrics:** 
- **Task Completion Rate (TCR):** What percentage of tasks did the agent complete successfully?
- **Action Efficiency:** Steps specific agent took compared to the oracle script?
- **Error Analysis:** Categorize **WHY** the agent failed. Is the agent misidentifying elements (perception error) or choosing the wrong action (logic error)?
