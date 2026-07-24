@'
import os
from dotenv import load_dotenv
from python_appfabric_oauth2_producer.config_setting import Settings
from python_appfabric_vault.vault import VaultBuilder

load_dotenv(dotenv_path=".env", override=True)

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

print("Vault read succeeded")
print("Vault key:", vault_key)
print("Returned field names:", sorted(vault_data.keys()))
'@ | py -
