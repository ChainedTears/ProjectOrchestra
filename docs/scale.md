1. **Define a set of canonical tasks:** Create a list of 20-30 common tasks you would do on a daily basis (e.g., login, search, add to cart, filling forms) across different websites
2. **Create "oracle" scripts:** The gold standard of perfectly written Playwright scripts we hope the AI will be able to generate. For each task, write a Playwright script with no errors using best Python practices. This will be our ground truth.
3. **Automate data collection:** We must have the perception module (`perception.py`) finished at this point. We will run the oracle scripts step by step, using the perception module to capture the state (`Sₜ` - State at time *t*), and execute the next command, (`Aₜ` - Action at time *t*). Then save `(Sₜ, Aₜ)` to dataset.
4. **Generate Variations:** Programmatically introduce variations in the tasks (different usernames, search queries, products) to increase dataset size and diversity.

# [BACK](README.md)
