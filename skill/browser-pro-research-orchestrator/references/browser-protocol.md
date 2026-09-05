# Browser execution and recovery

Read before sending or resuming research. Use only the available browser tool's documented operations. Resolve UI controls from fresh observed state, never from remembered element indices, guessed URLs, or fabricated selectors.

## Before each send

1. Confirm the signed-in Chrome destination and intended conversation/project. If the destination was not provided, use an unambiguous observed ordinary chat or project; otherwise ask. Preserve unrelated tabs and unfinished user drafts.
2. Check whether a response is still generating. Do not send into or change the model of a generating conversation. For a resumed or uncertain submission, inspect the recent messages before attempting another send.
3. Open the current model controls. For the default target, select **GPT-6 Astra and Pro** if not already selected. Verify the checked/selected state after the change. The controls may be combined or split across menus; do not assume a fixed order or UI spelling.
4. Establish both model family and mode from the actual controls. Treat `GPT-6 Pro` / `GPT-6 Astra Pro` as acceptable displayed labels only when the visible context unambiguously establishes the intended family and Pro mode. If a shortened or renamed label is ambiguous, inspect its UI details or official product documentation; do not guess a mapping. Honor a later explicit user target instead of the default.
5. Save the verification timestamp, exact observed labels, and a concise UI excerpt or cropped screenshot reference in the run log. Documentation or a Pro account badge alone is insufficient. If either selected family or mode is unobservable, withhold the send and report the exact limitation.
6. Close the menus without altering selection. Get a fresh page state, locate a unique composer and send control, and check the reviewed prompt against the intended workstream, context version, and existing draft.
7. Paste the reviewed prompt and verify that it is complete before sending. Check the tool mode: ordinary search is allowed; Deep Research stays off unless explicitly requested. Do not attach files or add sensitive material beyond authorization.
8. Send once. Confirm that the correct user message is visible and generation has started, or that a complete answer has already appeared. Record submission status/time and the observed conversation link. Do not infer success from a click alone.

Never silently downgrade to GPT-5.6 Pro, Auto, Thinking, Instant, or another family when access, quota, or tool capability is missing. Ordinary web search being unavailable does not authorize a mode switch; do primary-source verification locally and explicitly record that limitation. If the requested browser research itself cannot be done, report the blocker.

If a send is uncertain, inspect the conversation before retrying; an acknowledged user message is evidence to wait, not to duplicate it. An exact-target verification is required again before any actual resend. If a mismatch is discovered after sending, mark that exchange invalid for the required Pro consultation, preserve its provenance, and reissue on the verified target only when the task still needs it. Never relabel the invalid response.

## Waiting and capturing a complete response

Pro responses can take many minutes. Base polling on observed progress rather than treating any duration as proof of failure. As an initial heuristic, check after roughly five to ten minutes; back off toward fifteen to thirty minutes for long unchanged generations or follow a visible UI estimate. These are polling suggestions, not model latency guarantees.

- Do useful independent local research, source checking, or prompt preparation while waiting.
- Use a supported wakeable wait in short intervals, keeping individual blocking waits at or below sixty seconds so user steering and progress updates remain possible. Do not use blocking shell sleeps or tight repeated page refreshes.
- Create a recurring heartbeat or scheduled follow-up only when the user has requested/authorized waiting later, monitoring, or recurring work and the tool is available. A skill invocation alone does not authorize a new recurring automation. Prefer the current task's heartbeat to creating a standalone task.
- Save enough state for the monitor to resume the existing workstreams, review completed answers, and continue the authorized scope. Keep it quiet on unchanged/non-actionable state, notify on a meaningful change or required action, and stop the run's monitor on completion/cancellation. Respect current automation-tool instructions and existing notification preferences.
- If no scheduler is available, continue in the active turn with wakeable waits. If the session must end, save a precise checkpoint and state that work is pending; do not promise autonomous continuation without a real mechanism.
- While `Stop answering` or equivalent is visible, leave generation running. Never click `Answer now`, force a shortened answer, reload away from generation, or interrupt merely because it is slow.

Completion requires visible evidence that generation ended, not just a disappearing button during a navigation error. Read and capture the entire answer, including tables, caveats, sources, and any collapsed/continued content. Use the connector's supported reading/scrolling operations when the current view is truncated. Verify capture completeness before review; do not review only a tail or executive summary.

Record elapsed time, answer version, and capture status. If the model ended normally but omitted a required section, capture the answer as-is and request a focused completion after model verification; do not silently fill it in as model output.

## Interruptions and resumption

On a timeout, network failure, quota notice, login loss, or resumed task:

1. Read the run log, last prompt version, observed link, and last successful action.
2. Inspect the actual conversation and classify it as unsent, submitted/generating, complete/uncaptured, captured/unreviewed, or failed.
3. Continue from that state. Do not start duplicate chats or replay prompts simply because local memory is incomplete.
4. If the model is unavailable, save captured work and locally useful conclusions, state the blocker, and withhold further browser sends. Never bypass a limit by silently changing accounts or models.

When the browser connector requires tab finalization, finalize only task-created tabs as its documentation requires and make finalization the last browser operation of the turn. Do not close or repurpose user-owned tabs unnecessarily.
