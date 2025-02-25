![Outcome](/assets/connections/apps-menu.png)


### Add to Apps Menu
- If you have not customised the apps.jsp file for your connections environment, please make a copy of the file.

    - You can access the file from:

            <WAS_home>/profiles/<profile_name>/installedApps/<cell_name>/Homepage.ear/homepage.war/nav/templates/menu

    - Paste the copy into the common\nav\templates subdirectory in the customization directory:

            <installdir>\data\shared\customization\common\nav\templates\menu\apps.jsp

- To add the Kudos Boards app links add the following lines towards the bottom of the apps.jsp file before the `</table>` element, replacing `<BOARDS_URL>` with your URL

        --%><tr><%--
          --%><th scope="row" class="lotusNowrap"><%--
            --%><img width="16" src="https://<BOARDS_URL>/img/logo-small.png" /><%--
            --%><a href="https://[CONNECTIONS_URL]/boards/auth/connections"><%--
              --%><strong><fmt:message key="connections.component.name.kudos.boards" /></strong><%--
            --%></a><%--
          --%></th><%--
          --%><td class="lotusNowrap lotusLastCell"><%--
            --%><a href="https://[CONNECTIONS_URL]/boards/auth/connections?redirect_to=/todos/assigned"><%--
              --%><fmt:message key="label.menu.kudos.boards.todos" /><%--
            --%></a><%--
          --%></td><%--
          --%><td class="lotusNowrap lotusLastCell"><%--
            --%><a href="https://[CONNECTIONS_URL]/boards/auth/connections?redirect_to=/boards/templates/public"><%--
              --%><fmt:message key="label.menu.kudos.boards.templates" /><%--
            --%></a><%--
          --%></td><%--
        --%></tr><%--

    NOTE: `https://[CONNECTIONS_URL]/boards` is the same as that configured in the [Connections Header setup](/boards/connections/header-on-prem/#open-boards).

- Save and close the file

- Add the Kudos Boards Strings for the Apps Menu
    - Download the [strings files](/assets/strings.zip) and extract the files to the Connections strings customisation directory:

            <CONNECTIONS_CUSTOMIZATION_PATH>/strings

    - Note: Please append the lines to the files if they already exist. Extra languages can also be added

- The changes will take effect when the cluster(s) are restarted
