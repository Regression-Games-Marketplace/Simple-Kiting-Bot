# Deploying to RG

In order to deploy this to RG, you need to run the following steps:

1. Create a new bot on Regression Games, via zip file by zipping the contents of this repo.
2. Use the JSON in `publish.json` and make a POST call to `https://{RG_HOST}/bot/{ID}/publish`, where `ID` is the ID of the bot you created in step 1.
3. Within the database, update the description of the bot to be the content of the README.md file.