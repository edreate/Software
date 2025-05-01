## Code Contribution Guidelines for Edreate

## Setup Python
We use **uv** for Python version and dependency management:

```bash
pip install uv
uv venv --python 3.12
source .venv/bin/activate
```

After activating the environment, use the Makefile targets below.

---

### 1. Branching Strategy

- **Branch from `main`**: Always create a new branch off the latest `main`.
- **Naming conventions**:
  - Features: `feature/<short-description>` (e.g., `feature/user-authentication`)
  - Bug fixes: `bugfix/<short-description>` (e.g., `bugfix/fix-login-error`)
- **Never commit directly to `main`**: All work must be done in a feature or bugfix branch.

```bash
# Create a feature branch
git checkout main
git pull origin main
git checkout -b feature/your-branch-name
```

### 2. Keeping Your Branch Up to Date

- **Rebase regularly** to incorporate upstream changes from `main`:

```bash
# Fetch and rebase onto latest main
git fetch origin
git rebase origin/main
```

- Resolve any conflicts, test your changes, and continue the rebase:

```bash
# After resolving merge conflicts
git add <files>
# Continue the rebase
git rebase --continue
```

### 3. Pull Requests (PRs)

- Push your branch to GitHub and open a **Pull Request** against `main`.
- Assign reviewers and add a clear description of what your PR does.
- Ensure all checks pass (CI, linting, tests) before merging.
- **Squash and merge** to keep history clean or follow the project’s merge policy.

---

### 4. Python Type Hinting

- Use **strong type hints** for all functions, classes, and methods.
- Basic types:
  - `int`, `float`, `str`, `bool`, `list[int]`, etc.
- External types:
  - `cv2.typing.MatLike` for OpenCV image data
  - `PIL.Image.Image` for Pillow images

```python
from typing import List, Dict
import cv2
from cv2.typing import MatLike
from PIL import Image


def resize_image(image: MatLike, width: int, height: int) -> MatLike:
    """
    Resize an OpenCV image to the given width and height.

    :param image: Input image as a MatLike object
    :param width: Target width in pixels
    :param height: Target height in pixels
    :return: Resized image
    """
    return cv2.resize(image, (width, height))


def load_pillow_image(path: str) -> Image.Image:
    """Load an image from disk using Pillow."""
    return Image.open(path)
```

---

### 5. Naming Conventions

- Use **clear, descriptive names** for functions and variables.
- Functions should use **`snake_case`** and be verbs or verb phrases:
  - Good: `create_post()`, `add_two_numbers()`
  - Bad: `cp()`, `doIt()`

```python

def create_post(title: str, content: str) -> Dict[str, str]:
    """
    Create a new post object.

    :param title: Title of the post
    :param content: Body content of the post
    :return: Dictionary representing the new post
    """
    return {"title": title, "content": content}


def add_two_numbers(a: int, b: int) -> int:
    """
    Add two integers and return the result.

    :param a: First integer
    :param b: Second integer
    :return: Sum of a and b
    """
    return a + b
```

---

Following these guidelines will help maintain code quality, consistency, and a smooth review process across all our repositories. Thank you for contributing!

