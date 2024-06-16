pip install azure-identity azure-keyvault-secrets

```python
#Imports
#azure-identity
#azure-keyvault-secrets



from azure.identity import DefaultAzureCredential
from azure.keyvault.secrets import SecretClient
import pdb
import sys
import logging

# Create a new secret client
logging.getLogger("azure.identity").setLevel(logging.DEBUG)

# Create a stream handler that sends output to the console
handler = logging.StreamHandler(sys.stdout)
handler.setLevel(logging.DEBUG)

# Create a new root logger and add the stream handler
logger = logging.getLogger()
logger.addHandler(handler)

credential = DefaultAzureCredential()
client = SecretClient(vault_url="https://vps-vida-keys.vault.azure.net/", credential=credential)

# Retrieve the value of the secret
secret_name = "sf-user"
secret = client.get_secret(secret_name)
secret_value = secret.value
print(secret_value)
```