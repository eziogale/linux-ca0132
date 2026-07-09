When I bought a Gigabyte GA-Z170X-Gaming G1 motherboard back in 2016, I didn't do it for gaming, but rather for its audio purity. However, I was unaware of how much anti-Linux Creative had become.

It took me about a month just to get the rear panel line-out working. The solution came from a 2015 post by Takashi Iwai, which involved using the generic parser alongside a custom pintable found via `hdajacksensetest`. As Takashi noted at the time:

> "Some Sound Blaster Z models with the CA0132 codec don't work properly with the given firmware and its fixed mapping. Using the generic parser with a fixup instead makes such a board work more or less. Of course, you'll lose the features provided by the DSP firmware, but it's better than no output."

Since then, I've managed to keep both the mic and line-out working by recompiling the original patch with every kernel update. In 2018, I tried to get the audio working properly with Connor McAdams (using his [GitHub Repository](https://github.com/Conmanx360/QemuHDADump)), but we couldn't get it to work. As Connor added support for newer models, the `ca0132.c` file grew larger and larger, and eventually, the generic parser option I relied on so much was completely removed.

Porting this workaround to kernel 6.18.24 was so challenging that I felt compelled to share the patch. I hope this helps anyone else struggling with other broken models.

### Patch Link
[ALSA: hda/ca0132: add QUIRK_GENERIC path for Gigabyte GA-Z170X-Gaming G1](https://github.com/torvalds/linux/commit/e79615b05c78d19b085c8eb7971c82cb5b0f22d1)
