# ArgoCD GitOps on EKS

## What I built
A pull-based GitOps deployment using ArgoCD on AWS EKS, as a direct
comparison to my push-based GitHub Actions + ECS pipeline from the
previous lab.

## Architecture
Git push -> ArgoCD detects change (polls every 3 min) ->
ArgoCD pulls manifests -> applies to EKS cluster

## Push vs Pull comparison

Push-based (GitHub Actions + ECS):
- CI tool actively pushes the deploy
- Deploy credentials live outside the cluster, in CI
- No built-in drift detection

Pull-based (ArgoCD + EKS):
- Cluster pulls changes from Git itself
- Deploy credentials never leave the cluster
- Self-healing: manual cluster changes get auto-reverted to match Git

## What I proved hands-on
- Deployed an app purely by creating an ArgoCD Application object
- Scaled replicas 2 to 4 by only editing Git, never running kubectl apply
- Manually broke the deployment with kubectl scale --replicas=1
- ArgoCD self-healed it back to 4 replicas within seconds

## Cost
Total lab cost: under Rs 50, EKS cluster deleted after lab
'@ | Set-Content README.md

git add .
git commit -m "docs: add README comparing push vs pull CI/CD"
git push origin main