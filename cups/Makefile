srcdir=.
top_srcdir=..

apsdir=$(top_srcdir)/aps

serverbin=`cups-config --serverbin`
backenddir=$(serverbin)/backend
filterdir=$(serverbin)/filter

INSTALL=/usr/bin/install

CFLAGS+=-g -Wall -Wextra -Wmissing-prototypes -Wstrict-prototypes -Wmissing-declarations -Wshadow -I$(top_srcdir) `cups-config --cflags`
LDFLAGS+=-L$(apsdir) `cups-config --image --libs --ldflags` -l qrencode -lusb-1.0

TARGETS=rastertoaps texttoaps aps

all: $(TARGETS)

#utf8toaps: utf8toaps.c utf8.c text.c aps_fnt.c command.c options.c ticket.c $(apsdir)/libaps.a
#	@echo "Building $@..."
#	@$(CC) $(CFLAGS) $(LDFLAGS) $^ -o $@

rastertoaps: rastertoaps.c command.c options.c ticket.c $(apsdir)/libaps.a
	@echo "Building $@..."
	@$(CC) $(CFLAGS) $(LDFLAGS) $^ -o $@ $(LDFLAGS)

texttoaps: texttoaps.c utf8.c text.c aps_fnt.c command.c options.c ticket.c $(apsdir)/libaps.a
	@echo "Building $@..."
	@$(CC) $(CFLAGS) $(LDFLAGS) $^ -o $@ $(LDFLAGS)

aps: aps.c command.c options.c $(apsdir)/libaps.a
	@echo "Building $@..."
	@$(CC) $(CFLAGS) $(LDFLAGS) $^ -o $@ $(LDFLAGS)

clean:
	@$(RM) *.o $(TARGETS)

install:
	mkdir -p $(DESTDIR)$(backenddir) $(DESTDIR)$(filterdir)
	@$(INSTALL) -s aps $(DESTDIR)$(backenddir)
#	@$(INSTALL) -s utf8toaps $(filterdir)
	@$(INSTALL) -s rastertoaps $(DESTDIR)$(filterdir)
	@$(INSTALL) -s texttoaps $(DESTDIR)$(filterdir)
	
uninstall:
	@$(RM) $(DESTDIR)$(backenddir)/aps
	@$(RM) $(DESTDIR)$(filterdir)/rastertoaps
	@$(RM) $(DESTDIR)$(filterdir)/texttoaps
#	@$(RM) $(filterdir)/utf8toaps

