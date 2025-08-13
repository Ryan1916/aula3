


# varcredgit.py
import os

USER = "Ryan1916"
EMAIL = "lira.yryan@gmail.com"

name = os.popen("git config --global user.name").read().strip()
email = os.popen("git config --global user.email").read().strip()

if name == USER and email == EMAIL:
    print("✅ Credenciais já corretas")
else:
    os.system("git config --global user.name " + USER)
    os.system("git config --global user.email " + EMAIL)
    print("⚠️ Credenciais corrigidas para:")
    print(f"   user.name  = {USER}")
    print(f"   user.email = {EMAIL}")