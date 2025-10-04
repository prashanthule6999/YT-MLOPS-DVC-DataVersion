In MLOps, we are not only dealing with code, but also with data, models, and experiments. Traditional version control systems like Git are excellent for code, but they are not designed to handle large datasets, ML models, or experiment tracking. That’s where DVC comes in.

✅ Key Reasons to Use DVC in MLOps:
Data Versioning
Just like Git versions code, DVC versions datasets and ML models.
You can reproduce an experiment later with the exact same dataset and model used before.
Experiment Tracking
Keeps track of different training runs, parameters, metrics, and outputs.
Helps compare models easily (accuracy, loss, etc.).
Efficient Storage & Sharing
Large files (datasets, model binaries) are stored outside Git (e.g., S3, GCS, Azure Blob, local storage).
Git only tracks metadata (hashes), making repositories lightweight.
Reproducibility
Every experiment (data + code + parameters + environment) can be reproduced exactly.
Critical for debugging, auditing, or compliance.
Pipelines & Automation
DVC pipelines define data preprocessing, training, evaluation as reproducible stages.
Helzs automate workflows in CI/CD pipelines.
Team Collaboration
Data scientists and ML engineers can collaborate easily.
Everyone gets the same data/model versions without emailing zip files or manually syncing.

🔑 In short:
Git → version control for code
DVC → version control for data, models, and experiments
Together, they form the backbone of reproducible and collaborative MLOps.

-----------------------------------------------------------------------------------------------

# YT-MLOPS-DVC-DataVersion
This repo impliments the idea of data versioning using DVC tool.

1. Create git repo and clone it in local.
2. Create mycode.py clear and add code to it. (it will save a csv file to a new "data" folder)
3. Do a git add-commit-push before initializing dvc.
   pip install dvc
4. Now we do "dvc init" (creates .dvcignore, .dvc)
5. Now do "mkdir S3" (creates a new S3 directory)
6. Now we do "dvc remote add -d myremote S3"
7. Next "dvc add data/" 
   Now it will ask to do: ("git rm -r --cached 'data'" and "git commit -m "stop tracking data"")
   Because initially we were tracking data/ folder from git so now we remove it for DVC to handle.
8. Again we do "dvc add data/" (creates data.dvc) then "git add .gitignore data.dvc"
9. Now - "dvc commit" and then "dvc push"
9. Do a git add-commit-push to mark this stage as first version of data.
10. Now make changes to mycode.py to append a new row in data, check changes via "dvc status"
11. Again - - "dvc commit" and then "dvc push"
12. Then git add-commit-push (we're saving V2 of our data at this point)
13. Check dvc/git status, everything should be upto date.
14. Now repeat step 10-12 for v3 of data.
15. We can roll back to previous commit and data version doing following
	Check commit log by git log --oneline
	Then do git checkout SHA-ID will switch to previous commit
	Then do git status --> dvc status --> dvc pull this will pull data version push during git commit
