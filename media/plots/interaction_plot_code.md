```python
def perform_two_way_anova(df_input, alpha=0.05, slide_start_num=19):
    # Filter for Machine 1 and ensure column names are correct
    df_machine_1 = df_input[df_input['Machine'] == 1].copy()

    # Convert Pressure and Temperature to categorical types for statsmodels
    df_machine_1['Pressure'] = df_machine_1['Pressure'].astype('category')
    df_machine_1['Temperature'] = df_machine_1['Temperature'].astype('category')

    # Fit the OLS model for two-way ANOVA with interaction
    # C() notation treats variables as categorical
    model = ols('Resistance ~ C(Pressure) + C(Temperature) + C(Pressure):C(Temperature)', data=df_machine_1).fit()

    # Get the ANOVA table (Type 2 sums of squares is generally recommended for unbalanced designs)
    anova_table = sm.stats.anova_lm(model, typ=2)

    # --- Slide 19: Pressure (P) Significance ---
    print(f"### Slide {slide_start_num}: Display ANOVA Table / Pr(>F) for Pressure (P)")
    p_value_pressure = anova_table.loc['C(Pressure)', 'PR(>F)']
    print(f"ANOVA Table for Pressure:\n{anova_table.loc['C(Pressure)']}")
    print(f"\nText evaluation: Is this factor, P significant for Machine 1?")
    if p_value_pressure < alpha:
        print("Yes (p < 0.05)")
    else:
        print("No (p >= 0.05)")

    # --- Slide 20: Temperature (T) Significance ---
    print(f"\n### Slide {slide_start_num + 1}: Display ANOVA Table / Pr(>F) for Temperature (T)")
    p_value_temperature = anova_table.loc['C(Temperature)', 'PR(>F)']
    print(f"ANOVA Table for Temperature:\n{anova_table.loc['C(Temperature)']}")
    print(f"\nText evaluation: Is this factor, T significant for Machine 1?")
    if p_value_temperature < alpha:
        print("Yes (p < 0.05)")
    else:
        print("No (p >= 0.05)")

    # --- Slide 21: Pressure*Temperature (P*T) Interaction Significance ---
    print(f"\n### Slide {slide_start_num + 2}: Display ANOVA Table / Pr(>F) for Pressure*Temperature (P*T)")
    p_value_interaction = anova_table.loc['C(Pressure):C(Temperature)', 'PR(>F)']
    print(f"ANOVA Table for P*T Interaction:\n{anova_table.loc['C(Pressure):C(Temperature)']}")
    print(f"\nText evaluation: Is this factor, P*T significant for Machine 1?")
    if p_value_interaction < alpha:
        print("Yes (p < 0.05)")
    else:
        print("No (p >= 0.05)")

    # --- Slide 22: Interaction Plot ---
    print(f"\n### Slide {slide_start_num + 3}: Interaction Plot visualization showing the relationship between Pressure and Temperature on Machine 1 Resistance.")
    fig, ax = plt.subplots(figsize=(10, 6))
    interaction_plot(x=df_machine_1['Pressure'],
                     trace=df_machine_1['Temperature'],
                     response=df_machine_1['Resistance'],
                     ax=ax, legendloc='best') # Corrected parameter name
    ax.set_title('Interaction Plot of Resistance by Pressure and Temperature (Machine 1)', fontsize=16)
    ax.set_xlabel('Pressure', fontsize=12)
    ax.set_ylabel('Mean Resistance', fontsize=12)
    ax.grid(True, linestyle=':', alpha=0.7)
    plt.tight_layout()
    # plt.show() # Comment out plt.show() as we are saving to HTML

    # Save the matplotlib plot as an interactive HTML using mpld3 and plotly
    html_output = mpld3.fig_to_html(fig)
    # Now, save this HTML. For a fully interactive Plotly experience, one might convert to Plotly native if needed,
    # but mpld3 provides good interactivity for matplotlib figures.

    # Ensure media/plots directory exists
    os.makedirs('media/plots', exist_ok=True)

    plot_filename = 'interaction_plot.html'
    plot_filepath = os.path.join('media/plots', plot_filename)
    with open(plot_filepath, 'w') as f:
        f.write(html_output)

    print(f"✅ Interaction plot saved to {plot_filepath}")

    # Save the Python code to a markdown file
    code_filename = 'interaction_plot_code.md'
    code_filepath = os.path.join('media/plots', code_filename)
    with open(code_filepath, 'w') as f:
        f.write("```python\n")
        f.write(inspect.getsource(perform_two_way_anova)) # This will save the entire function code
        f.write("\n```")
    print(f"✅ Interaction plot code saved to {code_filepath}")

    # Add to slides.md
    with open('slides.md', 'a', encoding='utf-8') as f:
        f.write(f'''
---

:::: {{.columns}}
::: {{.column width="50%"}}
### Slide {slide_start_num+3}: Interaction Plot (Machine 1)

This plot visualizes the interaction effects of Pressure and Temperature on Machine 1's Resistance. The non-parallel lines suggest that the effect of one factor (e.g., Pressure) on Resistance depends on the level of the other factor (Temperature).

However, our ANOVA results indicated that the interaction (P*T) was *not* statistically significant (p-value = {p_value_interaction:.2f} >= 0.05), despite the visual appearance of non-parallel lines. This highlights the importance of statistical tests alongside visual inspection.
:::

::: {{.column width="50%"}}
<iframe
  data-src="media/plots/interaction_plot.html"
  width="100%"
  height="500px"
  style="border:none;"
  scrolling="no">
</iframe>
:::
::::
''')
    print("✅ Interaction plot slide added to slides.md")

```