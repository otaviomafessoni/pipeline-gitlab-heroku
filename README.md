# pipeline-gitlab-heroku

## CONFIGURAÇÃO CONSOLE HEROKU

Crie uma API KEY caso ainda não tenha na sua conta.

As variaveis utilizadas na pipeline:
HEROKU_PRODUCTION_KEY = API KEY
HEROKU_APP_NAME = nome do seu projeto

## PARA INSTALAR O RUNNER NO SEU GITLAB

https://docs.gitlab.com/runner/install/linux-manually.html
Using binary file

```bash
sudo chmod +x /usr/local/bin/gitlab-runner
```

```bash
sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash
```

```bash
sudo gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner
```

```bash
sudo gitlab-runner start
```

Para adicionar o runner ao seu projeto:

```bash
sudo gitlab-runner register
```

Utilize a URL do seu gitlab e o token gerado por ele

Depois desse passo execute o comando:

```bash
gitlab-runner verify
```

Caso precise execute novamente:

```bash
sudo gitlab-runner start
```

## CONFIGURAÇÕES DO GIT-RUNNER

```bash
nano /etc/gitlab-runner/config.toml
```

```javascript
concurrent = 1
check_interval = 0
shutdown_timeout = 0

[session_server]
  session_timeout = 1800

[[runners]]
  name = "NOMEDOSEURUNNER"
  url = "http://seugitlab.com/"
  token = "TOKEN_RUNNER"
  token_obtained_at = 2023-10-26T22:20:47Z
  token_expires_at = 0001-01-01T00:00:00Z
  executor = "docker"
  [runners.docker]
	tls_verify = false
	image = "docker:latest"
	privileged = true
	disable_cache = false
	volumes = ["/var/run/docker.sock:/var/run/docker.sock", "/cache"]
	shm_size = 0
	extra_hosts = [""]

  [runners.cache]
	MaxUploadedArchiveSize = 0
```
