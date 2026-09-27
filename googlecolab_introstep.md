import os
import sys
import glob

REPO_URL = "https://github.com/josenimo/HUPO_scverse_demo.git"
REPO_DIR = "HUPO_scverse_demo"

# 1. Clone & change directory
if not os.path.exists(REPO_DIR):
    !git clone --depth 1 {REPO_URL}
    %cd {REPO_DIR}
else:
    %cd {REPO_DIR}

# 2. Install uv binary
!curl -LsSf https://astral.sh/uv/install.sh | sh
os.environ["PATH"] = f"/root/.local/bin:{os.environ['PATH']}"

# 3. Sync to local .venv
!uv sync --no-install-project

# 4. Point Colab's active runtime to the .venv site-packages
venv_site_packages = glob.glob(f"{os.getcwd()}/.venv/lib/python*/site-packages")
if venv_site_packages:
    if venv_site_packages[0] not in sys.path:
        sys.path.insert(0, venv_site_packages[0])
    print(f"\n✓ Added {venv_site_packages[0]} to sys.path")

print("✓ Environment ready to import!")