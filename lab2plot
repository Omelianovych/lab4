import matplotlib.dates as mdates

s3 = boto3.client('s3')
s3.download_file('mybucket-perry', 'db.csv', 'downloaded.csv')

fig = plt.figure(figsize=(16, 5))
df = pd.read_csv('downloaded.csv')
df['exchangedate'] = pd.to_datetime(df['exchangedate'], format='%d.%m.%Y')
df = df.sort_values(by=['exchangedate'])
df.set_index('exchangedate', inplace=True)
df['date'] = df.index.strftime('%b %d')

plt.plot(df['date'], df['rate'])
plt.title('USD/UAH rate')
plt.xlabel('Date')
plt.ylabel('Rate')

months = mdates.MonthLocator()
plt.gca().xaxis.set_major_locator(months)
plt.gca().xaxis.set_major_formatter(mdates.DateFormatter('%b'))

plt.show()

fig.savefig('res.png')
s3.upload_file('res.png', 'mybucket-perry', 'res.png')
