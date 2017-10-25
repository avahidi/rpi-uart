
NAME = rpi-uart


all:
	@echo targets are clean, zip


clean:
#	rm -rf gerbers
	rm -rf $(NAME).zip

zip: gerbers
	rm -rf $(NAME).zip
	zip $(NAME).zip gerbers/*
