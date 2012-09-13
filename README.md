# Sublime Text 2 URI

This application allows you to directly open a file from your browser into Sublime Text 2.
For OSX only.

[Download the latest package here](https://github.com/pitpit/Sublime-Text-2-URI/downloads)

## Open a file traced into a Symfony2 Exception

Override a file `app/Resources/TwigBundle/views/Exception/trace.html.twig` containing:

    {% set replace = {"/mnt/workspace": "~/Workspace"} %}{# needed when the apache server do not use the same path tree than the developer desktop. ie: using VM) #}
    {% if trace.function %}
        at
        <strong>
            <abbr title="{{ trace.class }}">{{ trace.short_class }}</abbr>
            {{ trace.type ~ trace.function }}
        </strong>
        ({{ trace.args|format_args }})
    {% endif %}

    {% if trace.file is defined and trace.file and trace.line is defined and trace.line %}
        {{ trace.function ? '<br />' : '' }}
        in {{ trace.file|format_file(trace.line) }}
        {% spaceless %}
        <a href="edit://{{ trace.file|replace(replace) }}#{{ trace.line }}" title="Edit the file"><img style="vertical-align:top;" width="16" height="16" alt="star" src="data:image/gif;base64,R0lGODlhEAAQAMQAAORHHOVSKudfOulrSOp3WOyDZu6QdvCchPGolfO0o/XBs/fNwfjZ0frl3/zy7////wAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACH5BAkAABAALAAAAAAQABAAAAVVICSOZGlCQAosJ6mu7fiyZeKqNKToQGDsM8hBADgUXoGAiqhSvp5QAnQKGIgUhwFUYLCVDFCrKUE1lBavAViFIDlTImbKC5Gm2hB0SlBCBMQiB0UjIQA7" /></a>&nbsp;
        <a href="#" onclick="toggle('trace_{{ prefix ~ '_' ~ i }}'); switchIcons('icon_{{ prefix ~ '_' ~ i }}_open', 'icon_{{ prefix ~ '_' ~ i }}_close'); return false;">
            <img class="toggle" id="icon_{{ prefix ~ '_' ~ i }}_close" alt="-" src="{{ asset('bundles/framework/images/blue_picto_less.gif') }}" style="visibility: {{ 0 == i ? 'display' : 'hidden' }}" />
            <img class="toggle" id="icon_{{ prefix ~ '_' ~ i }}_open" alt="+" src="{{ asset('bundles/framework/images/blue_picto_more.gif') }}" style="visibility: {{ 0 == i ? 'hidden' : 'display' }}; margin-left: -18px" />
        </a>
        {% endspaceless %}
        <div id="trace_{{ prefix ~ '_' ~ i }}" style="display: {{ 0 == i ? 'block' : 'none' }}" class="trace">
            {{ trace.file|file_excerpt(trace.line) }}
        </div>
    {% endif %}

It adds an link (a star) on each trace line... Just click on it to open the file in your favorite editor !