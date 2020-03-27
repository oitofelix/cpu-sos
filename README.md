# cpu-sos
S.O.S. from a CPU in distress

‘cpu-sos’ is a buffer-local minor-mode designed to track the
visibility of buffers associated with sub-processes or EXWM managed
windows and send a SIGSTOP signal to those processes (and their
related ones) as soon as their buffers become buried, eventually
reverting this by sending a SIGCONT signal as soon as they become
visible again.  This has the effect of limiting CPU consumption of
processes managed by Emacs at the user’s discretion.  Useful for
programs whose background processing the user is not interested in.
For example, web-browsers running JavaScript aggressively on
background for no good reason.  Other legitimate use is to forcibly
disable background app notifications while one’s attention focus is
elsewhere.

CAVEATS: Notice that the concept of "visibility" used by this package
is defined by the semantics of the value ‘visible’ given to the
parameter ‘ALL-FRAMES’ of function ‘get-buffer-window’.  This is
necessary, but not sufficient for actual view of the buffer at hand.
For instance, if a buffer is in a window of a frame that is totally
occluded by another it still is regarded as "visible", although one
can’t actually see it.  Aside from imprecise detection of visual
interaction, there is no attempt to detect sound interaction.
Therefore, buffers running music players or recording programs should
not have this mode enabled.  The same is true if one wants to have
asynchronous processes delivering notifications at arrival.  Keep also
in mind that trying to yank selection from stopped processes is
problematic.
