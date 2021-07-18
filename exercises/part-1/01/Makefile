.PHONY: test clean

test: ./tests/1.fftrim.ogg ./tests/1.ffmpeg.ogg ./tests/2.fftrim.wav ./tests/2.ffmpeg.wav ./tests/3.fftrim.flac ./tests/3.ffmpeg.flac
	cmp ./tests/1.fftrim.ogg ./tests/1.ffmpeg.ogg
	cmp ./tests/2.fftrim.wav ./tests/2.ffmpeg.wav
	cmp ./tests/3.fftrim.flac ./tests/3.ffmpeg.flac

clean:
	rm -f ./tests/1.fftrim.ogg ./tests/1.ffmpeg.ogg ./tests/2.fftrim.wav ./tests/2.ffmpeg.wav ./tests/3.fftrim.flac ./tests/3.ffmpeg.flac

./tests/1.fftrim.ogg: ./tests/1.ogg
	fftrim -i $< -ss 1 -t 1 $@

./tests/1.ffmpeg.ogg: ./tests/1.ogg
	ffmpeg -hide_banner -loglevel error -nostats -i $< -ss 1 -t 1 -acodec copy $@

./tests/2.fftrim.wav: ./tests/2.wav
	fftrim -i $< -ss 1 -to 2 $@

./tests/2.ffmpeg.wav: ./tests/2.wav
	ffmpeg -hide_banner -loglevel error -nostats -i $< -ss 1 -to 2 -acodec copy $@

./tests/3.fftrim.flac: ./tests/3.flac
	fftrim -i $< -ss 0 -t 0.5 $@

./tests/3.ffmpeg.flac: ./tests/3.flac
	ffmpeg -hide_banner -loglevel error -nostats -i $< -ss 0 -to 0.5 -acodec copy $@
