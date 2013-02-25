OTHER_DIR=../../blog.mnewton.com/src
UNISON_OPTS=-auto -batch
SYNC_DIRS=templates contents/authors contents/css contents/img contents/js
SRC=$(shell find .)
BUILD_FILES=../archive ../articles ../css ../drafts ../img ../js ../*.html ../*.xml ../*.ico

ifdef M
	GIT_COMMIT_OPTS=-m "$(M)"
else
	GIT_COMMIT_OPTS=
endif

all: build push

build: 
	echo Running unison to sync changes
	echo
	$(foreach dir,$(SYNC_DIRS),unison $(UNISON_OPTS) ./$(dir) $(OTHER_DIR)/$(dir);)
	echo 
	echo running wintersmith
	echo
	wintersmith build
	
push:
	git add ..
	git commit $(GIT_COMMIT_OPTS)
	git push origin master

clean:
	rm -rf $(BUILD_FILES)

.PHONY: build push clean
