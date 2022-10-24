---

copyright:
  years: 2019, 2022
lastupdated: "2022-10-24"

keywords: autocompletion,auto-completion,spelling correction,autocorrection,auto-correction,type ahead,type-ahead

subcollection: discovery-data

---

{{site.data.keyword.attribute-definition-list}}

# Customizing the search bar
{: #search-bar}

Control how customers interact with the search bar.
{: shortdesc}

Decide whether the search bar can interact with customer query submissions in the following ways:

- Propose alternative search terms when a misspelling is detected
- Propose better query wording with type-ahead

These search bar customizations are available for all project types except *Conversational Search*. Similar features, such as autocorrection, can be configured for the chat widget where you deploy the project.
{: note}

To customize search bar behavior, complete the following steps:

1.  From the navigation pane, open the **Improve and customize** page.
1.  Expand **Customize display** from the *Improvement tools* pane, and then click **Search bar**.
1.  Turn the following features on or off by setting the associated switcher:

    Autocompletion
    :   As the customer types a word as part of a query into the search bar, completed words that make sense based on the project data are displayed as suggestions. The user can click a suggestion to add it to the query. This setting is enabled by default.

    Spelling suggestions
    :   Recognizes words that are misspelled in the customer query. After the query is submitted, a `Did you mean:` link is displayed that shows a corrected version of the original query. The customer can click the corrected query to submit it. This setting is disabled by default.
