OTHER_DIR=../../blog.mnewton.com/src
SYNC_DIRS=templates contents/authors contents/style contents/img contents/script
BUILD_FILES=$(shell find .. -type d \( -path '../src' -o -path '../.*' \) -prune -o -name '*' -not -name '.*' -print)
WINTERSMITH=../../wintersmith/bin/wintersmith


all: update sync build push


update:
	npm install
	npm update

sync:
	$(foreach dir,$(SYNC_DIRS),rsync -rau ./$(dir)/ $(OTHER_DIR)/$(dir)/ && rsync -rau $(OTHER_DIR)/$(dir)/ ./$(dir)/;)
	rsync -rau ./package.json $(OTHER_DIR)/package.json

build:
	$(WINTERSMITH) build
	
push:
	GIT_COMMIT_OPTS=-m "$(M)"
	# why doesn't this work?
	# ifdef M
	# 	GIT_COMMIT_OPTS=-m "$(M)"
	# else
	# 	echo "Commit details: ";\
	# 	read GIT_COMMIT_DETAILS
	# 	GIT_COMMIT_OPTS=-m $(GIT_COMMIT_DETAILS)
	# endif
	git add ..
	git add -u ..
	git commit $(GIT_COMMIT_OPTS)
	git push

preview: 
	$(WINTERSMITH) preview

clean:
	rm -rf $(BUILD_FILES)


.PHONY: update sync build push preview clean