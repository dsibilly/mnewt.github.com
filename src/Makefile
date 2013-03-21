OTHER_DIR=../../blog.mnewton.com/src
UNISON_OPTS=-auto -batch
SYNC_DIRS=templates contents/authors contents/css contents/img contents/js
SRC=$(shell find .)
BUILD_FILES=../archive ../articles ../css ../drafts ../img ../js ../*.html ../*.xml ../*.ico
HTML_FILES=$(shell find .. -not -path '../src/*' -not -path '*/.*' -name '*.html')

ifdef M
	GIT_COMMIT_OPTS=-m "$(M)"
else
	GIT_COMMIT_OPTS=
endif

all: update sync build push

update:
	npm install
	npm update

sync:
	$(foreach dir,$(SYNC_DIRS),unison $(UNISON_OPTS) ./$(dir) $(OTHER_DIR)/$(dir);)

build:
	node ./node_modules/wintersmith/bin/wintersmith build
	
push:
	git add ..
	git commit $(GIT_COMMIT_OPTS)
	git push

preview: 
	node ./node_modules/wintersmith/bin/wintersmith preview

clean:
	rm -rf $(BUILD_FILES)

.PHONY: update sync build push preview clean
	
