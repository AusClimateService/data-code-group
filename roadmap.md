# CaRSA Code Roadmap

This discussion paper attempts to descibe how we might go about
managing the code that underpins the data and information CaRSA makes available to end-users. 

## Step 1: Get all (or at least most of) our code in one place

As it currently stands,
the code associated with CaRSA is spread across
many different teams and individuals across a number of institutions.
While it probably won't be possible to have literally all our code in one place
(e.g. some code might be primarily used for other projects/collaborations),
the default should be for all CaRSA-related code to be hosted within the same GitHub organisation:  
https://github.com/ClimResAus

A GitHub organisation is essentially an umbrella under which to host a bunch of related GitHub repositories.
Having all our code in one place means that we can easily see what each other is working on
and thus hopefully collaborate across teams and institutions more effectively.
It also means we have a single place to point to if someone asks where the code is for CaRSA.

> **Moving code to a GitHub organisation**
>
> The process involved in moving code to a GitHub organisation
> depends on how that code is currently being managed:
> - If you've got an existing GitHub repository for your CaRSA-related work,
> you can transfer that GitHub repository to the new organisation following
> [these instructions](https://docs.github.com/en/github/administering-a-repository/transferring-a-repository)
> - If your local git repository isn't up on GitHub yet,
> you can create a new repository within the CaRSA organisation
> and then add that GitHub repository as a remote
> following [these instructions](https://docs.github.com/en/github/getting-started-with-github/managing-remote-repositories)


For those worried about privacy,
you can make your repositories within the CaRSA organisation private
(i.e. only members of the organisation will be able to see them)
and you can even change your settings so that your membership to the CaRSA organisation itself 
is only visible to other members of the organisation.
