# vault-secrets-to-files
A composite action that puts Hachicorp vault secrets to files

# Usage
    - name: Get secrets from hachicorp kv vault
      uses: ergrassa/vault-secrets-to-files@v1.0
            with:
              url: '${{ secrets.URL }}'
              token: '${{ secrets.TOKEN }}'
              engine: '${{ secrets.KV }}'
              path: 'somedir'
              debug: 'no'
- **`url`** is url of your vault, like `'http://your-vault.example.com'`
- **`engine`** is name of KV engine
- **`token`** is token that have at least _read_ access policy to the secret
- **`path`** _(optional)_ is base path where to put files, like `'/envs'`
- **`debug`** _(optional)_ if set to `'yes'` — will produce an output showing secret names, types and output path (values will be not exposed, only keys)

# Secrets special keys
- **`__filename__`** is file name to save that secrets, like `my_env_file.env`
- **`__type__`** says how to interpret the secret (details below)
- **`__path__`** is subpath where to put this file, like `my_envs`, it will be concat-ed with **`path`**

# Secret interpret
- **`json`** **(default)** will be saved as non-minified json
- **`env`** will be saved as `KEY=VAULE`
- **`yml`** or **`yaml`** will be saved as non-minified yaml
- **`txt`** or **`text`** is line-by-line text file, keys are line numbers
- **`file`** is base64-encoded file, it must have the keys `data` and `filename`, and `data` must start with `data:application/octet-stream;base64,`
