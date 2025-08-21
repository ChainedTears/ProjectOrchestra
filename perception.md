# Perception
We have learned from Agent SURF that presenting raw HTML only overcomplicate things and lead to countless hallucinations. Therefore, relying on just cleaned HTML is a fatal flaw. Because of how modern web pages are not just markup; but rather dynamic applications. Our state representation must be multi-modal.

## Simplified DOM Tree
Instead of presenting raw HTML, process the DOM into a simplified tree structure. Each node should contain it's tag, important attributes (`id`, `class`, `aria-label`, `role`), and a unique identifier assigned by this module. Interactable elements (`<button>`, `<input>`) must be explicitly flagged.

### OPTIONAL: Visual Context
We can attempt to finetune vision models to process visual layout with the DOM structure, results not guranteed.
