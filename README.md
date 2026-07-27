@'
import os
from dotenv import load_dotenv
from python_appfabric_oauth2_producer.config_setting import Settings
from python_appfabric_vault.vault import VaultBuilder

# Local test only: load the Vault connection variables.
load_dotenv(dotenv_path=".env", override=True)

alphasense_env_vars = [
    "ALPHASENSE_API_KEY",
    "ALPHASENSE_EMAIL",
    "ALPHASENSE_PASSWORD",
    "ALPHASENSE_CLIENT_ID",
    "ALPHASENSE_CLIENT_SECRET",
]

print("\n=== Managed Vault Verification ===")

print("\n1. AlphaSense credential variables before removal:")
for name in alphasense_env_vars:
    print(f"   {name}: {'present' if os.getenv(name) else 'not present'}")

# Remove AlphaSense credentials from the current Python process.
# This does not edit or delete anything from the .env file.
for name in alphasense_env_vars:
    os.environ.pop(name, None)

print("\n2. AlphaSense credential variables after removal:")
for name in alphasense_env_vars:
    print(f"   {name}: {'present' if os.getenv(name) else 'not present'}")

settings = Settings.get_instance().data
vault_key = settings["alphasense"]["vault_key"]

vault = (
    VaultBuilder()
    .set_cert_path(
        os.getenv("REQUESTS_CA_BUNDLE", os.getenv("SSL_CERT_FILE"))
    )
    .build()
)

vault_data = vault.get_secured_data(vault_key)

required_fields = set(alphasense_env_vars)
returned_fields = set(vault_data.keys())

print("\n3. Managed Vault result:")
print("   Vault read succeeded")
print("   Vault key:", vault_key)
print("   Returned field names:", sorted(returned_fields))

print(
    "\n4. All required AlphaSense credentials supplied by Vault:",
    required_fields.issubset(returned_fields),
)

print(
    "5. AlphaSense credentials are still absent from process environment:",
    all(os.getenv(name) is None for name in alphasense_env_vars),
)

print("\nVerification completed without displaying any secret values.")
'@ | py -
