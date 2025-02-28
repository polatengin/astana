# astana

## Project setup

Run the following command to create projects in the src folder;

```bash
npx create-next-app@latest --typescript --tailwind --eslint --app --use-npm --skip-install --disable-git --yes web-admin
npx create-next-app@latest --typescript --tailwind --eslint --app --use-npm --skip-install --disable-git --yes web-site
npx create-next-app@latest --typescript --tailwind --eslint --app --use-npm --skip-install --disable-git --yes web-supervisor
```

[pr.yml](./.github/workflows/pr.yml) file is created in the .github/workflows folder for the CI/CD process.

_Process changes_ step find the folders that has changes;

```bash
CHANGED_DIRS=$(git diff --name-only origin/${BASE_REF}..${HEAD_SHA} | \
               xargs -n1 dirname | \
               while read -r dir; do
                 for allowed in "${ALLOWED_PATHS_ARR[@]}"; do
                   if [[ "$dir" == "$allowed" || "$dir" == "$allowed"/* ]]; then
                     echo "$dir"
                     break
                   fi
                 done
               done | tr '\n' ' ' || true)
```

For each changed folder, the [./.iac/ingress.yml](./.iac/ingress.yml) file is updated with the random staging domain.

Also a comment is added (if there is no comment is added already) to the PR with the staging domains.

## Domains

Dev domains:

- Admin Panel : https://wdap.sample.com/ (src/web-admin)
- Supervisor Panel : https://wdsp.sample.com/ (src/web-supervisor)
- Website : https://wdws.sample.com/ (src/web-site)

Production domains:

- Admin Panel : https://admin.sample.com/
- Supervisor Panel : https://supervisor.sample.com/
- Website : https://sample.com/
