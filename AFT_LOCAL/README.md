# AFT_LOCAL

This folder contains the local-window Attention-Free Transformer experiment for WikiText language modeling.

## Files

- `AFT_LOCAL.ipynb`
  - Main notebook for model definition, data prep, training, evaluation, and text generation.

- `hyperparameter_sweep_results_aft_local_wiki.xlsx`
  - Spreadsheet with hyperparameter sweep outcomes for AFT-Local runs.
  - Use this file to compare settings and pick the best configuration.

## Functions and Classes in `AFT_LOCAL.ipynb`

### Model Components

- `AFTLocal(nn.Module)`
  - Core AFT-Local attention-free block.
  - Uses a local sliding-window mask plus causal masking.
  - Uses factorized positional bias (`u`, `v`) and stabilized exponentials (`K_stable`, `w_stable`) for numerical stability.

- `AFTLocal._create_local_mask(seq_len, window_size)`
  - Builds boolean mask where tokens only attend within local window and valid causal positions.

- `MLP(nn.Module)`
  - Feed-forward block with `Linear -> GELU -> Dropout -> Linear`.

- `AFTEncoderBlock(nn.Module)`
  - One encoder block with:
    - LayerNorm
    - `AFTLocal`
    - Residual + Dropout
    - LayerNorm
    - `MLP`
    - Residual + Dropout

- `AFT(nn.Module)`
  - Full model wrapper:
    - token embeddings
    - positional embeddings
    - stacked `AFTEncoderBlock` layers
    - final decoder projection to vocabulary logits.

### Data Pipeline

- `WikiTextDataset(Dataset)`
  - Holds pre-chunked token sequences and returns `(x, y)` shifted pairs for next-token prediction.

- `prepare_dataloaders(max_seqlen=64, batch_size=16, max_samples=5000, tokenizer_name="gpt2")`
  - Loads WikiText-103 train split.
  - Tokenizes text, chunks sequences, and creates train/val/test splits (80/10/10).
  - Returns dataloaders plus tokenizer.

### Training, Evaluation, and Generation

- `train_on_wiki()`
  - End-to-end training routine.
  - Creates dataloaders, builds model, trains for multiple epochs, and evaluates on validation data each epoch.
  - Logs train loss/perplexity and validation loss/perplexity/accuracy.
  - Returns `model`, `tokenizer`, and `test_loader`.

- `evaluate_test_set(model, test_loader, tokenizer, device)`
  - Final evaluation on unseen test split.
  - Reports test loss, perplexity, and token-level accuracy.

- `generate_text(model, tokenizer, prompt, max_new_tokens=100, device='cpu', temperature=0.4)`
  - Autoregressive text generation from a prompt using temperature-scaled sampling.

## Hyperparameter Tuning (AFT-Local)

Hyperparameter tuning happens in two places:

1. In-notebook baseline configuration inside `train_on_wiki()`:
   - `MAX_SEQLEN = 128`
   - `EMBED_DIM = 512`
   - `HIDDEN_DIM = 512`
   - `DEPTH = 5`
   - `BATCH_SIZE = 32`
   - `EPOCHS = 20`
   - `LR = 1e-4`
   - `WINDOW_SIZE = 32`

2. Sweep result tracking in `hyperparameter_sweep_results_aft_local_wiki.xlsx`:
   - Stores outcomes from multiple settings.
   - Used to compare runs and identify best-performing hyperparameter combinations for AFT-Local.

## Typical Workflow

1. Open `AFT_LOCAL.ipynb`.
2. Run model/data definition cells.
3. Run `train_on_wiki()` to train and validate.
4. Run `evaluate_test_set(...)` for final metrics.
5. Run `generate_text(...)` for qualitative testing.
6. Record/compare tuning results in `hyperparameter_sweep_results_aft_local_wiki.xlsx`.
