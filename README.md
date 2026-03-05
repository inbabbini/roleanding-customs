# Roleanding Customs V1.0

## Description

This repository contains custom D&D 5e content organized by content type. Each folder contains XML files formatted for Aurora Builder:

- **Classes** - Custom class and archetypes (subclasses)
- **Feats** - Custom feat definitions
- **Items** - Custom weapons, armor, shields, instruments, and general items
- **Races** - Custom playable races
- **Spells** - Custom spell definitions

## How to Use

1. Clone the repository locally, into your `$env:USERPROFILE\Docuemnts\5e Character Builder\custom\` folder by opening Powershell and running:
    - `cd $env:USERPROFILE\Docuemnts\5e Character Builder\custom\` 
    - `git clone https://github.com/inbabbini/roleanding-customs.git`
2. Open Aurora, make sure that it is configured to load custom content
3. ???
4. Profit

## How to Contribute

**Prerequisites:** You need to have a Github account and be added to this repository as a contributor. Ask me.

1. Create a new branch for your changes
    - `cd $env:USERPROFILE\Docuemnts\5e Character Builder\custom\roleanding-customs`
    - `git checkout -b "your_branch_name"`
2. Add or modify XML files in the appropriate content type folder. Make sure they work correctly by testing them in Aurora. Follow the guidelines stated in description to add your changes.
3. Add your contents to a new commit 
    - `git add .`
    - Verify all of your changes were added by running `git status`
4. Create the new commit to your local repository
    - `git commit -m"comment what you are adding"`
5. Push the new branch to the remote repository at Github (*)
    - `git push`
6. Go to Github, to the repository at https://github.com/inbabbini/roleanding-customs and create a Pull Request
7. Wait for your PR to be approved

**(*)** This will only work if you have locally configured your local git to work with your Github user

### Configure Git for Github

1. **Set your Git username and email** (for all commits on this machine):
   ```powershell
   git config --global user.name "Your Name"
   git config --global user.email "your.email@example.com"
   ```

2. **Choose an authentication method** (one of the following):

   **Personal Access Token**
   - Go to GitHub > Settings > Developer settings > Personal access tokens > Tokens (classic)
   - Generate a new token with `repo` and `gist` scopes
   - When pushing, use your GitHub username and the token as the password:
     ```powershell
     git push origin your_branch_name
     # When prompted for password, paste your personal access token
     ```
   - To avoid entering credentials repeatedly, configure Git credential manager:
     ```powershell
     git config --global credential.helper manager-core
     ```

3. **Verify your configuration**:
   ```powershell
   git config --global --list
   ```
   You should see your `user.name` and `user.email` listed.