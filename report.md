# Лабораторна робота 4 завдання 1.2

## Курс "Publish Packages" був успішно пройдений:

Файл **publish.yml**:

```yml
name: Publish to Docker
on:
  push:
    branches:
      - main
permissions:
  packages: write
  contents: read
jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      # Add your test steps here if needed...
      - name: Docker meta
        id: meta
        uses: docker/metadata-action@v5
        with:
          images: ghcr.io/hifichevymane/publish-packages/game
          tags: type=sha
      - name: Login to GHCR
        uses: docker/login-action@v3
        with:
          registry: ghcr.io
          username: ${{ github.repository_owner }}
          password: ${{ secrets.GITHUB_TOKEN }}
      - name: Build container
        uses: docker/build-push-action@v5
        with:
          context: .
          push: true
          tags: ${{ steps.meta.outputs.tags }}
```

Після цього в нас опублікувався образ проекту: https://github.com/hifichevymane/skills-publish-packages/pkgs/container/publish-packages%2Fgame

<img width="790" alt="Screenshot 2025-05-01 at 21 36 54" src="https://github.com/user-attachments/assets/63c91532-6b21-4d29-ae12-24789882bc02" />

Мені вдалося запустити образ на локальній машині:

<img width="536" alt="Screenshot 2025-05-01 at 21 24 58" src="https://github.com/user-attachments/assets/3c4bde24-acbb-4ae4-a5d8-a681b698d14a" />
<img width="808" alt="Screenshot 2025-05-01 at 21 27 04" src="https://github.com/user-attachments/assets/89e927fb-7604-45fd-96ea-28c26762da7c" />
<img width="799" alt="Screenshot 2025-05-01 at 21 27 36" src="https://github.com/user-attachments/assets/7eef1765-6754-45fc-8a53-446f79e3bc43" />
<img width="1440" alt="Screenshot 2025-05-01 at 21 30 05" src="https://github.com/user-attachments/assets/6da40bf0-236d-42e5-936f-0be76f5b1ca2" />


