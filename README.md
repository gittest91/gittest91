# Activate virtual environment
.\.venv\Scripts\Activate.ps1

# Load all variables from .env into the current PowerShell session
Get-Content .env |
Where-Object { $_ -match '^\s*[^#].*=' } |
ForEach-Object {
    $parts = $_ -split '=',2
    Set-Item -Path ("Env:" + $parts[0].Trim()) -Value $parts[1].Trim()
}

# Set local environment
$env:APP_ENV="local"

# Start the FastAPI application
py app.py


echo $env:APP_ENV


Dev Token Authenticated

py -c "import inspect; from investments_agentic_framework_adk.middleware import BearerAuthMiddleware; s=inspect.getsource(BearerAuthMiddleware); i=s.find('Dev Token Authenticated'); print(s[max(0,i-600):i+400])"

