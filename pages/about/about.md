---
title: About the author
---

{% include post-header.md %}

<script type="text/javascript">
    function hideId(id) {
        document.getElementById(id).style.display = 
            (document.getElementById(id).style.display === 'block') ? 'none' : 'block';
        document.getElementById(id + '-arrow').innerHTML =
            document.getElementById(id + '-arrow').innerHTML.replace(
                /show|hide/gi, 
                function(x) {return (x === 'show') ? 'hide' : 'show';}
            );
    }
</script>

I am currently a PhD candidate in the Department of Physics at the University of Maryland. [See my CV](media/cv.pdf).

{% include_relative education.md %}

{% include_relative projects.md %}

{% include_relative publications.md %}

{% include_relative presentations.md %}

{% include_relative appointments.md %}

{% include_relative personal.md %}

{% include top-button.html %}
