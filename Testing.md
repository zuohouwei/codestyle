
# Global, Local, Parameter Names

### Example
<table>
<tr><th width="400px">Good</th><th width="400px">Bad</th></tr>
<tr><td><pre lang="cpp">

void initLifecycle(
    ::lifecycle::Mode mode,
    ::lifecycle::Manager* pManager)
{
    ::lifecycle::Manager::TransitionResult result =
        ::lifecycle::Manager::TransitionResult::NONE;
}

</pre></td><td><pre lang="cpp">

void initLifecycle(
    ::lifecycle::Mode Md,
    ::lifecycle::Manager* ptr_mgr)
{
    ::lifecycle::Manager::TransitionResult r =
        ::lifecycle::Manager::TransitionResult::NONE;
}
</pre></td></tr>
</table>
