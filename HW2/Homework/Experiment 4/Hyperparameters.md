## Hyperparameters

1..5 | ForEach-Object {
    python cs285/scripts/run_hw2.py --env_name InvertedPendulum-v4 -n 100 `
    --exp_name "pendulum_discount_hyp_search_s$_" `
    -rtg --use_baseline -na `
    --discount 0.99 `
    --gae_lambda 0.99 `
    -s 256 `
    -l 3 `
    -lr 0.001 `
    -blr 0.002 `
    --batch_size 5000 `
    --baseline_gradient_steps 20 `
    --seed $_
}