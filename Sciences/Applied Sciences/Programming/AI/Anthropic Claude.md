
# Important Conceptual Remarks

## Anthropic's API vs Other APIs

Sources:
* s1: https://docs.anthropic.com/en/docs/build-with-claude/tool-use/overview#example-of-successful-tool-result:~:text=Differences%20from%20other%20APIs


Unlike APIs that separate tool use or use special roles like `tool` or `function`, Anthropic’s API integrates tools directly into the `user` and `assistant` message structure;

* Messages contain arrays of `text`, `image`, `tool_use`, and `tool_result` blocks. 
* `user` messages include client-side content and `tool_result`, 
* while `assistant` messages contain AI-generated content and `tool_use`.

