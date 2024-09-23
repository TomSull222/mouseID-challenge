# mouseID-challenge
I recieved outside help from a TA on these portions of my code listed from cells 26 thru 29
# Check for non-numeric entries in 'Weight (g)' and 'Tumor Volume (mm3)'
print(Capomulin_df[~Capomulin_df['Weight (g)'].apply(lambda x: str(x).isdigit())])
print(Capomulin_df[~Capomulin_df['Tumor Volume (mm3)'].apply(lambda x: str(x).replace('.', '').isdigit())])

# Remove rows with non-numeric data in 'Weight (g)' and 'Tumor Volume (mm3)'
# Capomulin_df['Weight (g)'] = pd.to_numeric(Capomulin_df['Weight (g)'], errors='coerce')
# Capomulin_df['Tumor Volume (mm3)'] = pd.to_numeric(Capomulin_df['Tumor Volume (mm3)'], errors='coerce')
# Capomulin_df['Mouse ID'] = pd.to_numeric(Capomulin_df['Mouse ID'], errors='coerce')
# Capomulin_df['Drug Regimen'] = pd.to_numeric(Capomulin_df['Drug Regimen'], errors='coerce')
# Capomulin_df['Sex'] = pd.to_numeric(Capomulin_df['Sex'], errors='coerce') 

# Drop rows with NaN values (which were previously non-numeric)
Capomulin_df = Capomulin_df.dropna(subset=['Weight (g)', 'Tumor Volume (mm3)', 'Mouse ID', 'Drug Regimen', 'Sex'])

# Generate a scatter plot of mouse weight vs. the average observed tumor volume for the entire Capomulin regimen
fig1, ax1 = plt.subplots()
cap_vol = Capomulin_df[['Mouse ID', 'Weight (g)', 'Tumor Volume (mm3)']].groupby(['Mouse ID']).mean().reset_index()
Capomulin_df[['Mouse ID', 'Weight (g)', 'Tumor Volume (mm3)']].groupby(['Mouse ID']).mean().reset_index()
marker_size = 15
plt.scatter(cap_vol['Weight (g)'], cap_vol['Tumor Volume (mm3)'], color='blue', s=marker_size)
plt.title('Mouse Weight Versus Average Tumor Volume')
plt.xlabel('Weight (g)', fontsize=14)
plt.ylabel('Average Tumor Volume (mm3)', fontsize=14)
plt.show() 
