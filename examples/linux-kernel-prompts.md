# Linux 示例：实际生成与局部修改提示词

使用内置图像生成功能。第一步将用户提供的原图作为风格与重新演绎参考；第二步使用第一张生成图；第三步使用第二张生成图。原始用户参考图未发布，生成结果也不保证逐像素可重现。

## 初次生成

```text
Use case: style-transfer
Asset type: Linux kernel source-code edition of the attached engineering meme.

Redraw the attached infrastructure meme into an ORIGINAL LINUX KERNEL SOURCE CODE MEME. The attached image is the style/comic-language reference: retain its thin shaky black pen, mostly flat pale gray filled blocks, huge white margins, utterly deadpan technical annotations, absurd asymmetric load-bearing, occasional tiny colored element. Replace the entire subject and layout with Linux-specific source-code visual jokes. This is an internet meme drawn casually by a kernel programmer, NOT a polished illustrated explainer, NOT a cute cartoon, NOT a mechanical engraving. Portrait 3:4. No large headline, no framing, no footnotes.

CENTRAL SILHOUETTE: a very tall dangerously off-center accretion of irregular gray rectangular blocks, ledges, stubs and narrow couplings, with subsidiary tiny towers emerging from big blocks. About 55% of canvas width. Main largest overhanging lump tagged "drivers/". Other shorter skewed blocks tagged "fs/", "net/", "mm/", "kernel/" with text sometimes along an edge, never arranged as a tidy floor-by-floor chart. The labels describe parts of source, not a dependency graph. A few unused small stubs and a patch held on by a bent paperclip make it look accreted, not designed. Sparse black contour lines: at most a few internal seams per block, no hatching, screws, gears or wooden scaffolding. Let the central silhouette look quietly impossible, like the reference.

THE TINY FOUNDATIONS: the giant bottom slab rests on a few hilariously puny mismatched parts on a plain wide foundation labelled "C". A central little linked wire pair, labelled "next" and "prev", with a curved annotation "struct list_head"; two other tiny supporting shims labelled "锁" and "页表" prevent the false impression that linked lists alone implement Linux. The two pointer wires are near the bottom, clearly in contact with the slab, bent under a comically disproportionate load. The main contrast is extremely serious sophisticated kernel machinery versus a few embarrassingly plain bookkeeping mechanisms. Do not write "全靠这玩意", do not explain the punchline.

INTEGRATED DEADPAN SIDE JOKES, drawn with very few lines and separated by generous white space:
1. Near the "mm/" block is a protruding bloated little rectangular process that sticks too far out. A tiny freestanding guillotine/saw labelled "OOM" is positioned to trim ONLY that process, not the supporting kernel. A short dangling scorecard on the selected piece says "oom_score". Tiny curved note says "按分处理". NO blood, faces, executioner, dice or random selection. The serious accounting label next to the brutal tiny tool is the joke.
2. A modest side outrigger from the central structure holds an old laptop labelled "MacBook5". A ridiculous long thin detour wire goes to its own very small reset button crudely taped onto the outrigger. Label the separate button "专用重启". This is a real model-specific reboot quirk, not a claim about all Macs. A tiny pale yellow strip of tape is the only color here.
3. High in the right margin, quite detached from the crowded structure, a tiny precision stopwatch is absurdly carefully mounted above an EMPTY tiny stool. Handwritten label "play_idle_precise()" and a second very short line "纳秒级发呆". A fine control wire connects it to the kernel apparatus. This denotes optional precise idle injection, not the kernel's foundation. No sleepy person, no dialogue.

A very small recognizable Tux penguin sticker may sit on the C foundation, deadpan, no talking or acting. Keep its yellow feet as one tiny color accent. No other characters, reaction faces, sweat, speech balloons, flying papers, confetti, caption explaining the humor, big LINUX title, marketing text, extra logos or invented code labels.
Typography must look casually handwritten, small but plainly legible, mixed source code names and concise Chinese annotations. Exact allowed labels: drivers/, fs/, net/, mm/, kernel/, C, next, prev, struct list_head, 锁, 页表, OOM, oom_score, 按分处理, MacBook5, 专用重启, play_idle_precise(), 纳秒级发呆.
The visual must remain sparse, rough, straight-faced and witty, NOT busy, adorable, glossy or aesthetically polished. Large boring gray masses, tiny precarious connectors, and specific weird attachments. This is a humorous metaphor, not an exact architecture diagram or source-size chart.
```

## 修正 1：让旁梗发生，消除错误连线

```text
Edit this Linux kernel meme. KEEP the existing white background, loose thin black outlines, gray fill, code labels, all three peripheral jokes, Tux sticker, blank margins, portrait framing. Do NOT add people, expressions, speech balloons, decorative details, hatching or a title.

Fix two visual problems:
1. The tiny next/prev wire-pair currently floats BELOW the load-bearing slab. It must be UNDER ACTUAL LOAD. Lower the huge slab until it clearly touches and bends the central linked wire-pair. Make the central list_head connector physically wedged between the huge slab and the C base, visibly flattened by the load. Keep the little '锁' and '页表' supports as other REAL supporting mechanisms, but reduce them to very thin, tiny precarious shims, so none looks like a strong safe pillar. All three small mechanisms should be in contact with the slab. Shift and lean the huge upper tower farther to the left relative to the tiny support cluster, looking outrageously off balance. The tiny foundations are all grossly disproportionate to what they support. Don't silently portray linked lists as Linux's only machinery.
2. The OOM tool should have JUST cut loose the side process, not stand idle beside an intact block. Make the outer rectangular block labeled 'oom_score' tilt and fall away from its connection, with two tiny severed links and minimal falling motion strokes; add the short label '进程' on that falling block. No blood or persons. Keep the very small tool marked OOM above the cut. DELETE the annotation '按分处理' and its arrow entirely. The score tag already communicates scoring; don't explain the joke.

Also REMOVE the long curved line from the 'net/' block to the precision-idle stool. Leave the stopwatch and empty stool as a strange isolated marginal apparatus with the existing accurate labels 'play_idle_precise()' and '纳秒级发呆'. It depicts a separate idle-injection routine, not a net/ dependency.

Everything else stays: MacBook5 with its absurd dedicated reset button; sparse angular gray mass; exact existing source names. It should look like a quietly impossible infrastructure doodle, never a neat modular infographic.
```

## 修正 2：支点接触

```text
Make ONE very small engineering correction to the supplied meme. Preserve every existing object, all upper architecture, all side jokes, every existing label, white space, exact framing, pen style, proportions and colors. Do not redraw the whole picture.

At the bottom center, the tiny curved next/prev wire object is floating below the huge gray slab. REPLACE ONLY THIS tiny wire object with TWO THIN CROOKED VERTICAL WIRE STRUTS. Each strut rises directly from the C foundation to TOUCH the UNDERSIDE OF THE GRAY SLAB above. There must be NO WHITE GAP between their top tips and the slab: draw the tips overlapping its black outline slightly. These wires visibly carry a little of the gigantic load alongside the existing tiny lock and page-table supports. Bow the wires slightly under pressure. Keep the next and prev labels aimed at the corresponding two struts. Add a very small curved annotation reading exactly "list_head" in the open white space to the left of this bottom support area, with a thin arrow to these struts.

Do NOT change or remove the '锁' or '页表' supports; do NOT remove 'next' or 'prev'. Do NOT change the falling oom_score process, OOM cutter, MacBook5 button, idle stool, Tux or C. Absolutely no new scene elements. This is only a small support-contact fix.
```
