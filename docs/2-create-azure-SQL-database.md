![A picture of the Microsoft Logo](./media/graphics/microsoftlogo.png)

# Create and Connect to an Azure SQL Database

The next section of the workshop you will be creating and connecting to an Azure SQL Database.

## Azure SQL Database create and connect workshop tasks

### Create a free Azure SQL Database

1. Ensure you have an Azure account to log into the Azure Portal. Need a free account? Sign up for one [here](https://azure.microsoft.com/en-us/free).

1. Navigate to the [Azure Portal](https://portal.azure.com/#home), and in the upper left corner, click the menu button.

    ![A picture of selecting the menu in the upper left corner of the Azure Portal](./media/ch2/deploy1a.png)

1. Then, select **Create a Resource**.

    ![A picture of selecting Create a Resource from the Azure Portal menu](./media/ch2/deploy1b.png)

1. In the category menu, select **Databases**.

    ![A picture of selecting Database from the category menu](./media/ch2/deploy1c.png)

1. Then click **create** for **SQL Database**.

    ![A picture of selecting create for SQL Database](./media/ch2/deploy1d.png)

1. On the **Create SQL Database** page, click the **Apply offer (Preview)** button for the free Azure SQL Database.

    ![A picture of clicking the Apply offer (Preview) button for the free Azure SQL Database on the Create SQL Database page](./media/ch2/deploy1e.png)

1. In the **Project details** section of the page, select a subscription and a Resource group if you have an existing one. 

    ![A picture of select a subscription and a Resource group on the Project details section of the page](./media/ch2/deploy1f.png)

    Otherwise you can create a Resource group by clicking the **Create new** button.

    ![A picture of creating a Resource group by clicking the **Create new** button](./media/ch2/deploy1g.png)

1. Next, in the **Database details** section of the page, name your database **freeDB** with the **Database name** field.

    ![A picture of naming your database with the Database name field in the Database details section of the page](./media/ch2/deploy1h.png)

1. For the **Server**, click the **Create new** button.

    ![A picture of naming your database with the Database name field in the Database details section of the page](./media/ch2/deploy1i.png)

1. On the **Create SQL Database Server** page, enter a **server name** and choose a **Location** using the dropdown menu.

    ![A picture of entering a server name and choosing a Location using the dropdown menu on the Create SQL Database Server page](./media/ch2/deploy1j.png)

1. Now, in the **Authentication** section, select the **radio button** for **Use Microsoft Entra-only authentication**.

    ![A picture of selecting the radio button for Use both SQL and Microsoft Entra authentication in the authentication section](./media/ch2/deploy1k.png)

1. Click the **Set admin** link in the **Set Microsoft Entra admin** section. 

    ![A picture of clicking the Set admin link in the Set Microsoft Entra admin section](./media/ch2/deploy1l.png)

1. Using the **Microsoft Entra ID** blade, find your user account and select it as an admin. Then click the **Select** button on the bottom left.

    ![A picture of select your account as the Entra ID admin](./media/ch2/deploy1m.png)

1. Click the **OK** button on the bottom left of the page.

    ![A picture of clicking the OK button at the bottom of the authentication page](./media/ch2/deploy1m1.png)

1. Back on the **Create a SQL Database** page, verify the values you entered and that the free database offer has been applied. 

    ![A picture of verifying the values and that the free database offer has been applied](./media/ch2/deploy1o.png)

1. On the top of the page, click on the **Additional settings** tab.

    ![A picture of clicking on the Additional settings tab](./media/ch2/deploy11a.png)

1. On the Additional settings page, find the **Data source** section on the top.

    ![A picture of the Data source section on the Additional settings page](./media/ch2/deploy11b.png)

1. Use the **Use existing data** toggle

    ![A picture of the Use existing data toggle](./media/ch2/deploy11c.png)

    to set it to **Sample** by clicking on it.

    ![A picture of clicking on the sample option of the Use existing data toggle](./media/ch2/deploy11d.png)

    and in the pop-up doalog, select **OK** for the question **"Do you want to continue"**.

    ![A picture of selecting OK for the question Do you want to continue in the pop-up doalog](./media/ch2/deploy11e.png)

1. On the bottom of the page in the lower left, click the **Review + create** blue button.

    ![A picture of clicking the Review + create blue button](./media/ch2/deploy11f.png)

1. On the following page, click the **Create** button in the lower left.

    ![A picture of clicking the Create button in the lower left](./media/ch2/deploy1p.png)

1. The following page will detail the deployments progress.

    ![A picture of the database deployment progress page](./media/ch2/deploy1q.png)

1. Once the deployment is done, click the blue **Go to resource** button to see your database details.

    ![A picture of clicking the blue Go to resource button to see your database details on the database deployment progress page](./media/ch2/deploy1r.png)

#### Network access to the database

1. On the database details page, the right hand side, you will see the **Server name** field with a link the your database server. Click the server name link.

    ![A picture of clicking the server name link on the database details page](./media/ch2/deploy1s.png)

1. Click the **Networking** link on the left hand side menu in the **Security** section.

    ![A picture of clicking the Networking link on the left hand side menu in the Security section](./media/ch2/deploy1t.png)

1. On the **Networking** page, click the **radio button** next to **Selected networks**.

    ![A picture of clicking the radio button next to Selected networks on the networking page](./media/ch2/deploy1u.png)

1. In the **Firewall rules** section, click the button labeled **"Add your client IPv4 address (X.X.X.X)"** to add your local IP address for database access.

    ![A picture of clicking the button labeled "Add your client IPv4 address (X.X.X.X)" to add your local IP address for database access](./media/ch2/deploy1v.png)

1. Click the **checkbox** for **Allow Azure services and resources to access this server** in the **Exceptions** section.

    ![A picture of clicking the checkbox for Allow Azure services and resources to access this server in the Exceptions section](./media/ch2/deploy1w.png)

1. Finally, click the **Save** button in the lower left of the page.

    ![A picture of clicking the save button in the lower left of the page](./media/ch2/deploy1x.png)

### Connect to the free Azure SQL Database

#### Option 1: Using the Query Editor in the Azure Portal

1. Using the menu on the left side, open the menu items under **Settings** if not alreay opened. Then select **SQL Databases** by clicking on it.

    ![A picture of clicking the SQL Databases option under settings](./media/ch2/deploy2a.png)

1. Next, on the main page, find the FreeDB you created and click on it naviage to the database details page.

    ![A picture of clicking the FreeDB SQL Databases](./media/ch2/deploy2b.png)

1. Using the menu options on the left side, find and click on **Query editor (preview)**.

    ![A picture of clicking on Query editor (preview) in the left menu](./media/ch2/deploy2c.png)

1. Next, click on the blue **Continue as ...** (with ... being the user you set as the database admin upon creation) in the Microsoft Entra authentication section.

    ![A picture of clicking on Microsoft Entra authentication continue as user blue button](./media/ch2/deploy2d.png)

1. The Query Editor will be used in the following chapters for running T-SQL code and procedures.

    ![A picture of the query editor](./media/ch2/deploy2e.png)

#### Option 2: Using Azure Data Studio

1. Azure Data Studio is another option for working with the database with a dedicated client tool. To use this tool, start on the main page, **Getting Started** tab for the database details. Here click on the blue **Open Azure Data Studio** button.

    ![A picture of clicking on the blue Open Azure Data Studio button](./media/ch2/deploy3a.png)

1. On the following page, if Azure Data Studio is not installed, click on the blue **Download Azure Data Studio** button to start that process. If it is already installed or was just installed, click on the **Launch it now** link.

    ![A picture of downloading or launching Azure Data Studio from the Azure portal](./media/ch2/deploy3b.png)

1. The link will launch Azure Data Studio and pre-create a database connection profile with the database details for the Azure SQL Database that was just created. Start by changing the **Authentication Type** to **Microsoft Entra ID**.

    ![A picture of changing the Authentication Type to Microsoft Entra ID](./media/ch2/deploy3c.png)

1. For the **Account** field, if you have been authenticated previously, an email address will be present. Select your email address for the account field. Once the profile is filled out, click the blue **Connect** button.

    ![A picture of selecting your email address for the account field](./media/ch2/deploy3d.png)

1. If no account has been set/logged in, select the **Add an account** option and authenticate via the Azure portal.

    ![A picture of selecting the Add an account option and authenticate via the Azure portal](./media/ch2/deploy3e.png)

1. Once connected to the database, right click on the connection name in the connection navigator on the left side and choose **New Query**.

    ![A picture of right clicking on the connection name in the connection navigator on the left side and choosing New Query](./media/ch2/deploy3f.png)

