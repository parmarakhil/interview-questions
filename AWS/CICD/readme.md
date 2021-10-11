# CICD

1. Code Commit
    1. A fully-managed source control service that hosts secure Git-based repositories, similar to Github.
    2. You can create your own code repository and use Git commands to interact with your own repository and other repositories.
    3. You can store and version any kind of file, including application assets such as images and libraries alongside your code.
    4. The AWS CodeCommit Console lets you visualize your code, pull requests, commits, branches, tags and other settings.
    5. You can migrate a Git repository to a CodeCommit repository in a number of ways: by cloning it, mirroring it, or migrating all or just some of the branches.
    6. You can also migrate your local repository in your machine to CodeCommit.
    7. You can transfer your files to and from AWS CodeCommit using HTTPS or SSH. For HTTPS authentication, you use a static username and password. For SSH authentication, you use public keys and private keys.
    8. Your repositories are also automatically encrypted at rest through AWS KMS using customer-specific keys.
    9. You can give users temporary access to your AWS CodeCommit repositories through a number of methods: SAML, Federation, Cross-Account Access, or through third party authorizes with Amazon Cognito.
2. Code Build
    1. A fully managed continuous integration service that compiles source code, runs tests, and produces software packages that are ready to deploy.
    2. A build project defines how CodeBuild will run a build. It includes information such as where to get the source code, which build environment to use, the build commands to run, and where to store the build output.
    3. A build environment is the combination of operating system, programming language runtime, and tools used by CodeBuild to run a build.
    4. The build specification is a YAML file that lets you choose the commands to run at each phase of the build and other settings. Without a build spec, CodeBuild cannot successfully convert your build input into build output or locate the build output artifact in the build environment to upload to your output bucket.
        1. If you include a build spec as part of the source code, by default, the build spec file must be named buildspec.yml and placed in the root of your source directory.
    5. A collection of input files is called build input artifacts or build input and a deployable version of a source code is called build output artifact or build output.