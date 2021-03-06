[.NET 用 Microsoft Azure Configuration Manager ライブラリ](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) には、構成ファイルの接続文字列を解析するためのクラスが用意されています。 [CloudConfigurationManager クラス](https://msdn.microsoft.com/library/azure/mt634650.aspx) を使用すると、クライアント アプリケーションがデスクトップ、モバイル デバイス、Azure 仮想マシン、Azure クラウド サービスのいずれで実行されているかにかかわらず、構成設定を解析できます。

CloudConfigurationManager パッケージを参照するには、次の `using` ステートメントをクラスに追加します。

    using Microsoft.Azure;    //Namespace for CloudConfigurationManager

構成ファイルから接続文字列を取得する方法の例を次に示します。

    // Parse the connection string and return a reference to the storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("StorageConnectionString"));

Azure Configuration Manager の使用はオプションです。 また、.NET Framework の [ConfigurationManager クラス](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx)などの API を使用することもできます。



<!--HONumber=Nov16_HO2-->


