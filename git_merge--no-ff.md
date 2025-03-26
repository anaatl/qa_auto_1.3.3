Вот пример того, как использовать команду `git merge --no-ff` в терминале:

### 1. **Создаём два репозитория (или две ветки)**

Допустим, у тебя есть репозиторий с основной веткой `main`, и ты хочешь создать новую ветку, где будешь делать изменения.

```bash
git init my-project
cd my-project
```

Создаём файл и делаем первый коммит в ветке `main`:

```bash
echo "Hello, world!" > hello.txt
git add hello.txt
git commit -m "Add hello.txt"
```

Теперь создаём новую ветку, например `feature-branch`, и переключаемся на неё:

```bash
git checkout -b feature-branch
```

Изменяем файл в ветке `feature-branch`:

```bash
echo "New feature!" > hello.txt
git add hello.txt
git commit -m "Add feature to hello.txt"
```

### 2. **Переключаемся обратно на `main` и вносим изменения**

```bash
git checkout main
echo "Updated content in main branch" > hello.txt
git add hello.txt
git commit -m "Update hello.txt in main branch"
```

### 3. **Теперь объединяем ветки с командой `--no-ff`**

Когда ты хочешь объединить изменения из `feature-branch` в `main`, используешь команду с флагом `--no-ff`:

```bash
git merge --no-ff feature-branch
```

### Что происходит:
- Git создаст новый коммит, который объединяет изменения из `feature-branch` в `main`, **сохраняя информацию о том, что это было объединение** (merge).
- Если бы ты использовал обычный `git merge feature-branch`, Git мог бы просто "приклеить" изменения без отдельного коммита, если не было конфликтов. Но с `--no-ff` всегда создается новый коммит, показывающий, что это объединение.

### 4. **Проверка истории коммитов**

Чтобы увидеть, что произошло, можно проверить историю коммитов:

```bash
git log --oneline
```

Ты увидишь коммиты в виде:

```
<new_commit_id> Merge branch 'feature-branch'
<commit_id> Update hello.txt in main branch
<commit_id> Add hello.txt
```

Таким образом, команда `git merge --no-ff` всегда сохраняет историю объединений и делает её более понятной, даже если можно было бы сделать это без лишних шагов.
