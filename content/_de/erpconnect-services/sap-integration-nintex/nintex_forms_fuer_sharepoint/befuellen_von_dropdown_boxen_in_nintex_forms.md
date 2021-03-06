---
ref: ecs-sin-nintex-forms-02
layout: page
title: Befüllen von Dropdown-Boxen in Nintex-Forms
description: Befüllen von Dropdown-Boxen in Nintex-Forms
product: erpconnect-services
parent: nintex_forms_fuer_sharepoint
permalink: /:collection/:path
weight: 2
lang: de_DE
old_url: /ERPConnect-Services-DE/default.aspx?pageid=bef_llen_von_dropdown_boxen_in_nintex_forms
---

In bestimmten Integrationsszenarien kann es sinnvoll sein, SAP-Daten für eine flexible Datenselektion in kaskadierenden Dropdown-Listen zur Verfügung zu stellen. Auch dies ist mit JavaScript und ECS REST-Services in Nintex Forms möglich (vgl. vorheriges Beispiel).

Im vorliegenden Beispiel soll in einem Eingabefeld eine SAP Materialnummer eingegeben und die möglichen Treffer in einer Dropdownliste angezeigt werden. Wird ein Material in der Dopdown-Liste selektiert, dann soll der Materialtext in einem weiteren Feld angezeigt werden. 

**Schritt 1: Textfelder definieren**

In unserer Nintex-Form benötigen wir drei Felder mit Bezeichnungen: 

1. Das erste Feld *Material Number* vom Typ **Single Line Textbox** ist das Eingabefeld und enthält die Materialnummer.
2. Im zweiten Feld *Suggested Materials* vom Typ **Choice** werden die möglichen Treffer für die eingegebene Materialnummer in einer Dropdownliste ausgegeben und sind selektierbar.
3. Im dritten Feld *Material* vom Typ **Single Line Textbox** wird der Material-Langtext zum ausgewählten Material angezeigt.

![nintex-forms-js-dropdown-01](/img/content/nintex-forms-js-dropdown-01.jpg){:class="img-responsive"}

Rufen Sie zunächst die Settings für das Feld *Material Number* auf und setzen Sie die Option *Store Client ID in JavaScript Variable* auf Yes. <br>
Tragen Sie *field_input* als Namen ins Feld *Client ID JavaScript variable name* ein.

![nintex-forms-js-dropdown-02](/img/content/nintex-forms-js-dropdown-02.jpg){:class="img-responsive"}

Rufen Sie anschließend die Settings für das *Choice*-Feld auf. <br>
Wählen Sie als Anzeigeformat Drop down list und tragen Sie bei *Choices* z.B. Start typing ein. Was Sie hier eintragen spielt keine Rolle, da die Eingabe durch JavaScript später wieder überschrieben wird (Im vorliegenden Beispiel mit dem Satz *Start typing in the input* above).  
Setzen Sie anschließend die Option *Store Client ID in JavaScript Variable* auf Yes und tragen Sie ins Feld *Client ID JavaScript variable name* den Name *field_select* ein.

![nintex-forms-js-dropdown-03](/img/content/nintex-forms-js-dropdown-03.jpg){:class="img-responsive"}

Rufen Sie anschließend die Settings für die *Single Line Textbox* neben *Material* auf. Setzen Sie auch hier die Option *Store Client ID in JavaScript Variable* auf Yes und tragen Sie ins Feld *Client ID JavaScript variable name* den Name *field_output* ein.   

Da es sich nur um ein Anzeigefeld handeln soll, können Sie zusätzlich unter *Appearance* definieren, dass das Feld nur angezeigt werden soll und keine Eingaben zugelassen sind.        

![nintex-forms-js-dropdown-04](/img/content/nintex-forms-js-dropdown-04.jpg){:class="img-responsive"}

**Schritt 2: JavaScript-Code einfügen**

Fügen Sie eine Referenz zu unserer JavaScript-Bibliothek unter *Form Settings -> Advanced -> Custom JavaScript Includes* ein:

[http://static.theobald-software.com/theobald.ecs.micro/5.2.0/theobald.ecs.micro.js](http://static.theobald-software.com/theobald.ecs.micro/5.2.0/theobald.ecs.micro.js)


![nintex-forms-js-dropdown-05](/img/content/nintex-forms-js-dropdown-05.jpg){:class="img-responsive"}

Fügen Sie den JavaScript-Code unter *Form Settings -> Advanced -> Custom JavaScript* ein.

![nintex-forms-js-dropdown-06](/img/content/nintex-forms-js-dropdown-06.jpg){:class="img-responsive"}

Im Code wird die Funktion *tEcs.executeXql* aufgerufen, um die Materialnummer und den Material-Langtext aus der SAP-Tabelle MAKT zu lesen.

{% highlight javascript %}
NWF$(document).ready(function() {
    theobald.ready(function() {
        var $ = NWF$,
            // material number input and dropbox
            tsInput = $('#' + field_input),
            tsSelect = $('#' + field_select),
            // description output
            tsInputDescription = $('#' + field_output),
            //
            // literals
            strings = {
                loading: 'Loading...',
                matches: ' matches',
                noMatchText: 'No direct match!',
                noMatches: 'No matches',
                errComm: 'Communication error, please see console',
                select: 'Please select',
                type: 'Start typing in the input above'
            },
            //
            //selectOptionString = '{0} ({1})',
            domOptionString1parameter = '{0}',
            domOptionString = '{0} ({1})',
            // xql query
            xqlString = "SELECT TOP 10 MATNR, MAKTX FROM MAKT WHERE (MATNR LIKE '%{0}%' OR MAKTX LIKE '%{0}%') AND SPRAS = 'EN'",
            queryFunction = function(val) {
                return tEcs.executeXql({
                    data: tEcs.format(xqlString, val)
                });
            };
 
        tsSelect.empty();
        tsSelect.append(tEcs.format(domOptionString1parameter, strings.type));
 
        tsInput.on('input', function() {
            tsSelect.empty();
            tsSelect.append(tEcs.format(domOptionString1parameter, strings.loading));
            queryFunction(tsInput.val())
                .done(function(data) {
                    tsSelect.empty();
 
                    if (data.length > 0) {
                        tsSelect.append(tEcs.format(domOptionString, strings.select, data.length + strings.matches));
                        $.each(data, function(i, v) {
                            var $option = $(tEcs.format(domOptionString, v.MATNR, v.MAKTX));
                            $option.attr('tsdescription', v.MAKTX);
                            tsSelect.append($option);
                        });
                    } else {
                        tsSelect.append(tEcs.format(domOptionString1parameter, strings.noMatches));
                    }
                }).fail(function(xhr, et) {
                    console.log(xhr, et);
                });
        });
        tsSelect.on('change', function() {
            var firstOption = tsSelect.find('option:first');
            if (firstOption.val() === strings.select) {
                firstOption.remove();
            }
 
            tsInput.val(tsSelect.val());
            tsInputDescription.val(tsSelect.find('option:selected').attr('tsdescription'));
        });
    });
});
{% endhighlight %}

Für weitere Informationen siehe [JavaScript Library for REST](../../ecs-de/ecs-runtime/ecs-webservices/javascript-bibliothek-fuer-rest).<br>  
Dieses Szenario können Sie auch mit ECS Core umsetzen, siehe [Developing with ECS Core](../../ecs-core/anwendungsentwicklung-mit-ecs-core).

**Schritt 3: Die Nintex Form ausführen**

Nun führen Sie die Form aus und geben Sie eine Materialnummer ein. Die Treffer zur Eingabe werden aus SAP gelesen und in der Dropdown Liste (Suggested Materials) angezeigt.  


![nintex-forms-js-dropdown-07](/img/content/nintex-forms-js-dropdown-07.jpg){:class="img-responsive"}

Wählt man ein Material aus der Liste aus, wird der Langtext dazu im Feld *Material angezeigt*. 

![nintex-forms-js-dropdown-08](/img/content/nintex-forms-js-dropdown-08.jpg){:class="img-responsive"}
