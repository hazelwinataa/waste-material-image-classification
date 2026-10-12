# Experiment evidence and methodological considerations

Evidence comes from **two team notebooks**, the supplied poster, and an earlier report. The report documents the baseline and improved CNN; the later notebook and poster also include MobileNetV2 V1 and V2. Notebook outputs were inspected, **not re-executed**.

## Test-set metrics (380 images)

| Model | Accuracy | Keras test precision | Keras test recall | Classification-report macro F1 | Classification-report weighted F1 |
|---|---:|---:|---:|---:|---:|
| Baseline CNN | 0.547368 | 0.739362 | 0.365789 | 0.55 | 0.55 |
| Improved CNN | 0.802632 | 0.871473 | 0.731579 | 0.80 | 0.80 |
| MobileNetV2 V1 | 0.813158 | 0.840456 | 0.776316 | 0.78 | 0.81 |
| MobileNetV2 V2 | 0.797368 | 0.806630 | 0.768421 | 0.78 | 0.80 |

**Macro F1 and weighted F1 are different averaging schemes.** The poster presents rounded F1 values and should not be interpreted as a uniformly specified independent metric series. The Keras precision/recall metrics printed by `model.evaluate` on one-hot multi-class labels should not be mistaken for macro-average per-class precision or recall. Per-class metrics are preserved in the notebook classification reports.

## Test classification insights

- Baseline to Improved CNN: glass recall 0.33 → 0.74; macro F1 0.55 → 0.80.  Baseline epochs 10; improved was allowed up to 30, making comparison not strictly budget-matched.
- MobileNetV2 V1 test accuracy 81.32%, weighted F1 0.81; trash recall 0.55.
- MobileNetV2 V2 test accuracy 79.74%, weighted F1 0.80; trash recall 0.65. Its stronger rare-class recall does not imply uniformly improved classification.
- V1 and V2 use ImageNet-pretrained MobileNetV2 with an initial frozen-backbone phase followed by selective fine-tuning. Their recorded class weights and regularization differ.

## Evaluation limitations

1. The `train_test_split` stratified 70/15/15 setup produces distinct train (1,768), validation (379) and test (380) rows. No cross-partition perceptual-hash check for near-duplicate images was documented.
2. Experiment candidates were compared using test metrics. Selecting a winner from test-set results can make the selected model's reported performance optimistically biased. Future selection should use validation only, followed by a single untouched test evaluation.
3. The baseline and improved CNN received different training budgets (10 vs maximum 30 epochs), so improvements cannot be assigned to architecture or class weighting alone.
4. Data augmentation, class weights, and transfer learning can all affect accuracy; no controlled factorial ablation isolates their individual contributions.
5. Grad-CAM displays informative regions but is not proof of causal model reasoning; some failures attend to backgrounds.
6. Notebook code was syntax-checked but not retrained for this publication. The original image files and `.keras` checkpoints are not included.
7. The source work was produced by a **BINUS University student team**; no solo ownership of the entire experiment is claimed.

## Source notebook handling

The actual executed code cells and core evaluation outputs are preserved in `notebooks/`. A handful of very large repetitive embedded image galleries were removed to keep GitHub rendering practical; selected original plots were extracted to `figures/`. The notebooks may require small environment/path adjustments and the original dataset before reproducing training.
