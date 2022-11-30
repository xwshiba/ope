# OPEN EDUCATION (OPE) Test Image

## About Test Image
The test image is designed to include the general features of OPE image that deployed in BUROSA (Boston University RHODS-AWS) dev environment. It is intended to be deployed in BUROSA test environment, serving as a CI/CD support for the general OPE image.

## Test Image Alterations
The test image has been altered to satisfy the test purpose because we are leveraging [RHODS ods-ci](https://github.com/xwshiba/ods-ci) for OPE image tests. 
Compared with the dev image, here are the alterations:

- `Dockerfile`
  - Removed the step of overriding Jupyterlab json file
  - Rewired the static customize part for it to correctly reference `ope_uid`, `ope_gid` and `ope_group`.
- `jupyter_disable_exts`
  - Removed all Jupyterlab disabled extensions
- `python_pkgs`
  - Added `jupyterlab-git` tool to use RHODS tests without alter their launcher files

## Test Image Customization
The image build process is driven by the `Makefile`. It will use the settings in the `base` folder. Regarding the documentation of `Makefile`, please reference the `main` branch. 
If you ever need to make a new OPE image using this repository, please double-check the following key files before using `make` commands:
- `ope_uid`, `ope_gid` and `ope_group`
  - Ideally, it needs to match the uid of the container deployment platform. However, it also needs to coordinate with `ope_gid` and `ope_group`. For example, if you set `ope_gid` as 0 and `ope_group` as root, it is ok to set `ope_uid` as 1000 and deploy it successfully.
- `ope_book`
  - You can change it to match your book/course name.
- `ope_book_registry`
  - You can change it to use your preferred registry.
- `ope_book_user`
  - Make sure to coordinate it with `ope_book_registry`, as you need write access to push the built image to your registry.

## More Questions
If you have more questions, please let us know through opening an issue.