
1. **Create a New Repository in Azure DevOps:**
    
    - First, you need to create a new repository in your Azure DevOps project. Log in to your Azure DevOps account, navigate to your project, and create a new repository.
    https://dev.azure.com/VarianCloud/Proton-Therapy-Vida
    

1. **Get the URL of Your Azure DevOps Repository:**
    
    - After creating the repository, you'll be provided with its URL. This URL is what you'll use to set the new remote in your local repository. It usually looks like this: `https://dev.azure.com/VarianCloud/<YourProject>/_git/<YourRepository>`.
3. **Change the Remote URL in Your Local Repository:**
    
    - Open your terminal or command prompt.
    - Navigate to the root directory of your local git repository.
    - First, remove the existing remote pointing to GitHub. You can do this with the following command:
        
        arduinoCopy code
        
        `git remote remove origin`
        
    - Next, add the new remote pointing to your Azure DevOps repository using the following command. Replace the URL with your Azure DevOps repository URL.
        
        phpCopy code
        
        `git remote add origin https://dev.azure.com/<YourOrganization>/<YourProject>/_git/<YourRepository>`
        
    - To verify that the remote has been set correctly, you can list the remote connections of your repository:
        
        Copy code
        
        `git remote -v`
        
        This command should now display the URL of your Azure DevOps repository associated with the `origin` remote.
4. **Push Your Code to the Azure DevOps Repository:**
    
    - If your Azure DevOps repository was created empty, you could push your local repository to Azure DevOps with the following command:
        
        `git push -u origin --all`
        
    - This command pushes all your branches to the new remote repository and sets the upstream tracking references. The `-u` flag associates your local branches with the remote branches, making future pushes/pulls simpler.