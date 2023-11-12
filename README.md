# FVC
Fast Video Codec. 

# Glossary

Macroblock: 8x8 image block

Macroblock diff: Should we define img1, and img2 as images, then the macroblock diff is the macroblocks in img2 that are different from the macrolock in the same position in img1, with the difference calculated using a set difference function.
                  The difference function doesn't always have to be both macroblocks are exact, because that would make the video lossless. If otherwise (the difference function doesn't require the macroblocks to be exact), then the video compression is lossy.

previous frame number: the (n+1)th previous frame going from 0 to 60. If n is 0, then n+1 = 1, so if you go backwards from this current frame number n+1 times, you get that frame's number.

# I-Frame

Frame with uncompressed data.

Starts with 0x01, then frame length (width * height * stride) (uint, 64-bit, big-endian), then frame data.

# D-Frame

Frame compressed by only storing the macroblock diff between one of the previous 60 frames.

Starts with 0x01, then previous frame number that this macroblok diff is referencing to, then the number of macroblocks in the macroblock diff, then previous then frame length (width * height * stride) (uint, 64-bit, big-endian), and last frame data (each macroblock in the frame data starts with a 32-bit number dictating which macroblock in the macroblock diff is this macroblock).

