# Datalad with GitHub LFS special remote

```bash
datalad create -c text2git datalad-github
cd datalad-github
head -c 100 /dev/urandom >random.bin
datalad save -m "data: add random data" random.bin
datalad create-sibling-github --access-protocol ssh datalad-github
datalad push --to github
git annex initremote github-lfs type=git-lfs url=git@github.com:iimog/datalad-github.git encryption=none embedcreds=no
git annex copy --to=github-lfs random.bin
datalad push --to github
```

This works. You can clone it and get the data from GitHub
```bash
cd ..
datalad clone git@github.com:iimog/datalad-github.git datalad-github-clone
cd datalad-github-clone
datalad get random.bin
```
