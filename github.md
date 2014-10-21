GitHub Cheatsheet 
=====
## Adding Multiple ssh keys (on Mac)
1. Create new key <code>ssh-keygen rsa -C "email address for account"</code>
2. Don't overwrite your keys. Give each key its own name. For example <code>id_rsa_Account1</code> and <code>id_rsa_Account2</code>. Or just give your primary account id_rsa and name the other accounts accordingly.
3. Attach the new key. 
  	1. Open the <code>id_rsa_AccountName.pub</code> file. Copy the string from that file. 
  	2. Login to GitHub
  	3. Click Settings (top right)
  	4. Click the SSH keys link (left hand nav)
  	5. Click the "Add SSH key" button
  	6. Provide title like "home computer"
  	7. Paste string into "key" field
4. Create a config file
	1. <code>touch ~/.ssh/config</code>
	2. <code>subl ~/.ssh/config</code>
	3. Create 2 entries, the first should entry is your default github account and the second should be your secondary account. The config file should look something like this:
	
<pre><code>#Default Account
Host github.com
  HostName github.com
  User [username1]
  IdentityFile ~/.ssh/id_rsa
  IdentitiesOnly yes
   
#Secondary Account
Host github-SECONDARY
  HostName github.com
  User [username2]
  IdentityFile ~/.ssh/id_rsa_Account2
  IdentitiesOnly yes
</code></pre>

Make sure you add the ```IdentitiesOnly yes```. This is neccessary to make sure that you don't log into a GitHub account and get "stuck" with it. 

To add remote repository using that secondary account

<code>git remote add origin git@github-SECONDARY:account2/repoName.github.io.git</code>