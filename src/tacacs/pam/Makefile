.ONESHELL:
SHELL = /bin/bash
.SHELLFLAGS += -e

MAIN_TARGET = libpam-tacplus_$(PAM_TACPLUS_VERSION)_amd64.deb
DERIVED_TARGETS = libtac2_$(PAM_TACPLUS_VERSION)_amd64.deb \
		  libtac-dev_$(PAM_TACPLUS_VERSION)_amd64.deb

$(addprefix $(DEST)/, $(MAIN_TARGET)): $(DEST)/% :
	# Obtain pam_tacplus
	rm -rf ./pam_tacplus
	git clone https://github.com/jeroennijhof/pam_tacplus.git 
	pushd ./pam_tacplus
	git checkout -f v1.4.1

	# Apply patch
	git apply ../0001-Don-t-init-declarations-in-a-for-loop.patch
	git apply ../0002-Fix-libtac2-bin-install-directory-error.patch

	dpkg-buildpackage -rfakeroot -b -us -uc
	popd

	mv $(DERIVED_TARGETS) $* $(DEST)/

$(addprefix $(DEST)/, $(DERIVED_TARGETS)): $(DEST)/% : $(DEST)/$(MAIN_TARGET)
