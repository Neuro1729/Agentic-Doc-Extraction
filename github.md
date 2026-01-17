
```markdown
# Transfer only `medical/` folder from another GitHub repo to your repo (Windows CMD)

:: Step 0: Delete old temp folder (if it exists)
rmdir /S /Q %USERPROFILE%\temp-medical

:: Step 1: Create a fresh temporary folder and enter it
mkdir %USERPROFILE%\temp-medical
cd %USERPROFILE%\temp-medical

:: Step 2: Initialize an empty git repo and add the source repo
git init
git remote add origin https://github.com/https-deeplearning-ai/sc-landingai.git

:: Step 3: Enable sparse checkout (only fetch specific folder)
git config core.sparseCheckout true

:: Step 4: Specify the folder to pull (medical/)
echo medical/ > .git\info\sparse-checkout

:: Step 5: Pull only that folder from source repo
git pull origin main
:: If the source repo uses 'master' instead of 'main', use:
:: git pull origin master

:: Step 6: Go to home folder and clone your destination repo
cd %USERPROFILE%
git clone git@github.com:Neuro1729/Agentic-Doc-Extraction.git

:: Step 7: Copy the 'medical' folder into your repo
xcopy /E /I %USERPROFILE%\temp-medical\medical %USERPROFILE%\Agentic-Doc-Extraction\medical

:: Step 8: Commit the changes in your repo
cd %USERPROFILE%\Agentic-Doc-Extraction
git add medical
git commit -m "Add medical module from sc-landingai"

:: Step 9: Push to GitHub
git push origin main
:: If your repo uses 'master' instead of 'main', replace 'main' with 'master'

:: Step 10: Optional cleanup - remove temp folder
rmdir /S /Q %USERPROFILE%\temp-medical
```

