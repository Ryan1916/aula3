


# Nome do Projeto

Descrição breve do projeto.

# varcredgit.py
import subprocess

# Credenciais corretas
MEU_USERNAME = "Ryan1916"
MEU_EMAIL = "lira.yryan@gmail.com"

def git_config_get(key):
    """Obtém o valor de uma chave de configuração do git."""
    try:
        result = subprocess.check_output(
            ["git", "config", "--global", key],
            text=True
        ).strip()
        return result
    except subprocess.CalledProcessError:
        return None

def git_config_set(key, value):
    """Define uma chave de configuração do git."""
    subprocess.run(["git", "config", "--global", key, value])

def git_config_unset(key):
    """Remove uma chave de configuração do git."""
    subprocess.run(
        ["git", "config", "--global", "--unset", key],
        stdout=subprocess.DEVNULL, stderr=subprocess.DEVNULL
    )

def main():
    # Obter credenciais atuais
    current_name = git_config_get("user.name")
    current_email = git_config_get("user.email")

    print(f"Credenciais atuais:\n  Nome: {current_name}\n  Email: {current_email}")

    # Checar se já são as corretas
    if current_name == MEU_USERNAME and current_email == MEU_EMAIL:
        print("✅ Credenciais já estão corretas.")
        return

    print("⚠️ Credenciais incorretas ou não configuradas. Ajustando...")

    # Remover as atuais (se existirem)
    if current_name and current_name != MEU_USERNAME:
        git_config_unset("user.name")
    if current_email and current_email != MEU_EMAIL:
        git_config_unset("user.email")

    # Definir as credenciais corretas
    git_config_set("user.name", MEU_USERNAME)
    git_config_set("user.email", MEU_EMAIL)

    print("✅ Credenciais configuradas com sucesso!")

if __name__ == "__main__":
    main()