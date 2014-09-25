
KEYRING_NAME=apt.thequux.com.gpg

KEYS = $(wildcard keys/*.asc)

build: build/$(KEYRING_NAME)
build/$(KEYRING_NAME): $(KEYS)
	[ -d build ] || mkdir -p build
	[ -f $@ ] && rm -f $@ || true
	touch $@
	gpg --keyring $@ --import $^

install: build
	install -d $(DESTDIR)/etc/apt/trusted.gpg.d
	install -d $(DESTDIR)/etc/apt/sources.list.d
	install -o root -g root -m 0755 \
	    build/$(KEYRING_NAME) $(DESTDIR)/etc/apt/trusted.gpg.d/
	install -o root -g root -m 0755 \
	    00-apt.thequux.com.list $(DESTDIR)/etc/apt/sources.list.d/
