
## Technical requirements

Your computer should have an internet connection, and at least 8 GB RAM and 50 GB free disk space.

## UNIX

As is stated in the course prerequisites at the [announcement web page](https://www.sib.swiss/training/), we expect participants to have a basic understanding of working with the command line on UNIX-based systems. You can test your UNIX skills with a quiz [here](https://docs.google.com/forms/d/e/1FAIpQLSd2BEWeOKLbIRGBT_aDEGPce1FOaVYBbhBiaqcaHoBKNB27MQ/viewform?usp=sf_link). If you don't have experience with UNIX command line, or if you're unsure whether you meet the prerequisites, follow our [online UNIX tutorial](https://edu.sib.swiss/pluginfile.php/2878/mod_resource/content/4/couselab-html/content.html). Before the course, make sure you can comfortably work with command line, R and git repository.

## Software

Most of the exercises will be run on [Gitpod](https://www.gitpod.io/). Here are the steps to log in on Gitpod:

1. Create a [github](https://github.com/) or a [gitlab](https://about.gitlab.com/) account.
Remember your email, your username, and your password!

<figure>
  <img src="../../../assets/images/general/gitpod1.jpg" align="center" width="300"/>
</figure>

2. Open [Gitpod](https://www.gitpod.io/) and link your GitLab Account

<figure>
  <img src="../../../assets/images/general/gitpod2.jpg" align="center" width="300"/>
</figure>

Authenticate your login with your gitlab/github credentials!

<figure>
  <img src="../../../assets/images/general/gitpod3.jpg" align="center" width="300"/>
</figure>

3. Open the desired repository in Gitpod: add `gitpod.io/#` at the beginning of the repository URL or...

	* Click [here]() to directly open Day1 repo in Gitpod
	* Click [here](https://gitpod.io/#https://gitlab.com/evogenlab/teaching-repos/biodivinfo) to directly open Day2 repo in Gitpod
	* Click [here]() to directly open Day3 repo in Gitpod

<!-- AT. You will also need a location version of [R]() installed on your computer -->

## Using Gitpod

You can find the entire Gitpod documentation [here](https://www.gitpod.io/docs/introduction).

### Reminders

* Only files in the `/workspace` directory are kept between state transitions (when you stop and restart a workspace), so don’t store files anywhere else otherwise they will be deleted when you stop the workspace
* Always stop workspace before leaving, otherwise it will keep running and be billed!
	* 'Menu' (the 3 horizontal bars top-left of the window)
	* 'Gitpod: Stop workspace' (lower half of the menu)


### Troubleshooting

* If you have a problem with your browser not showing everything, blocking pop-ups... click [here](https://www.gitpod.io/docs/configure/user-settings/browser-settings) for help
* If you have a problem when authenticating through gitlab, github or bitbucket, click [here](https://www.gitpod.io/docs/configure/authentication) for help
* If the text you enter in the Gitpod terminal is invisible, try deactivating the GPU acceleration:
	* Click on the cog in the bottom-left
	* ‘Settings’
	* Type ‘gpu acceleration’ in the search bar
	* Set ‘Terminal › Integrated: Gpu Acceleration’ to off’
