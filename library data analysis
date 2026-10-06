import pandas as pd
import matplotlib.pyplot as plt
from matplotlib.gridspec import GridSpec



# 1. LOAD DATA


file_name = "library_books.csv"

df = pd.read_csv(file_name)

# Remove unnecessary spaces from column names
df.columns = df.columns.str.strip()

# Convert required columns to numeric
df["Rating"] = pd.to_numeric(df["Rating"], errors="coerce")
df["Publication_Year"] = pd.to_numeric(df["Publication_Year"], errors="coerce")



# 2. BASIC ANALYSIS


total_books = len(df)

average_rating = df["Rating"].mean()

total_genres = df["Genre"].nunique()

total_authors = df["Author"].nunique()

genre_count = df["Genre"].value_counts()

rating_count = df["Rating"].value_counts().sort_index()

year_count = df["Publication_Year"].value_counts().sort_index()

author_count = df["Author"].value_counts().head(10)

most_common_genre = genre_count.idxmax()
most_common_genre_count = genre_count.max()

highest_rating = df["Rating"].max()

highest_rated_book = df.loc[
    df["Rating"].idxmax(), "Book_Name"
]



# 3. CREATE DASHBOARD


fig = plt.figure(figsize=(18, 12))

fig.patch.set_facecolor("white")

# Grid layout
# NOTE: top/bottom/left/right are set explicitly so the grid never
# collides with the fig.text() header/KPI block placed in absolute
# figure coordinates above it. hspace is increased so row-2 titles
# don't overlap row-1 x-axis labels.
gs = GridSpec(
    4,
    2,
    figure=fig,
    height_ratios=[0.05, 2.5, 2.5, 1.6],   # row 3 (Key Insights) enlarged so its
                                            # three lines of text have room to
                                            # breathe instead of overlapping
    hspace=1.3,    # was 0.75 — that wasn't enough room for row-2 chart
                   # titles to clear row-1's x-axis labels, so they overlapped
    wspace=0.30,
    top=0.74,      # nudged down slightly since the header block below is taller
    bottom=0.05,
    left=0.06,
    right=0.97
)


# 4. MAIN TITLE


fig.suptitle(
    "LIBRARY BOOK DATA ANALYZER",
    fontsize=20,
    fontweight="bold",
    y=0.97
)

fig.text(
    0.5,
    0.905,         # much bigger gap below the title now (was 0.045, now 0.065)
    "Python for Data Science - Data Analysis Dashboard",
    ha="center",
    fontsize=13
)



# 5. KPI SECTION


# Total Books
fig.text(
    0.15, 0.85,
    "TOTAL BOOKS",
    ha="center",
    fontsize=14,
    fontweight="bold"
)

fig.text(
    0.15, 0.815,
    str(total_books),
    ha="center",
    fontsize=19,
    fontweight="bold"
)


# Average Rating
fig.text(
    0.38, 0.85,
    "AVERAGE RATING",
    ha="center",
    fontsize=14,
    fontweight="bold"
)

fig.text(
    0.38, 0.815,
    f"{average_rating:.2f}",
    ha="center",
    fontsize=19,
    fontweight="bold"
)


# Total Genres
fig.text(
    0.62, 0.85,
    "TOTAL GENRES",
    ha="center",
    fontsize=14,
    fontweight="bold"
)

fig.text(
    0.62, 0.815,
    str(total_genres),
    ha="center",
    fontsize=19,
    fontweight="bold"
)


# Total Authors
fig.text(
    0.85, 0.85,
    "TOTAL AUTHORS",
    ha="center",
    fontsize=14,
    fontweight="bold"
)

fig.text(
    0.85, 0.815,
    str(total_authors),
    ha="center",
    fontsize=19,
    fontweight="bold"
)



# 6. BOOKS BY GENRE


ax1 = fig.add_subplot(gs[1, 0])

genre_count.sort_values().plot(
    kind="barh",
    ax=ax1
)

ax1.set_title(
    "Books by Genre",
    fontsize=16,
    fontweight="bold",
    pad=12
)

ax1.set_xlabel("Number of Books", fontsize=11)
ax1.set_ylabel("Genre", fontsize=11)

ax1.tick_params(axis="both", labelsize=9)

ax1.grid(
    axis="x",
    alpha=0.25
)

ax1.set_axisbelow(True)



# 7. RATING DISTRIBUTION


ax2 = fig.add_subplot(gs[1, 1])

rating_count.plot(
    kind="bar",
    ax=ax2
)

ax2.set_title(
    "Rating Distribution",
    fontsize=16,
    fontweight="bold",
    pad=12
)

ax2.set_xlabel("Rating", fontsize=11)
ax2.set_ylabel("Number of Books", fontsize=11)

ax2.tick_params(
    axis="x",
    rotation=45,
    labelsize=8
)

ax2.grid(
    axis="y",
    alpha=0.25
)

ax2.set_axisbelow(True)


# 8. BOOKS BY PUBLICATION YEAR


ax3 = fig.add_subplot(gs[2, 0])

ax3.plot(
    year_count.index,
    year_count.values,
    marker="o",
    linewidth=2
)

ax3.set_title(
    "Books by Publication Year",
    fontsize=16,
    fontweight="bold",
    pad=8
)

ax3.set_xlabel(
    "Publication Year",
    fontsize=11
)

ax3.set_ylabel(
    "Number of Books",
    fontsize=11
)

ax3.grid(
    True,
    alpha=0.25
)

ax3.tick_params(
    axis="both",
    labelsize=9
)



# 9. TOP 10 AUTHORS

ax4 = fig.add_subplot(gs[2, 1])

author_count.sort_values().plot(
    kind="barh",
    ax=ax4
)

ax4.set_title(
    "Top 10 Authors",
    fontsize=16,
    fontweight="bold",
    pad=8
)

ax4.set_xlabel(
    "Number of Books",
    fontsize=11
)

ax4.set_ylabel(
    "Author",
    fontsize=11
)

ax4.tick_params(
    axis="both",
    labelsize=8
)

ax4.grid(
    axis="x",
    alpha=0.25
)

ax4.set_axisbelow(True)


# 10. KEY INSIGHTS


ax5 = fig.add_subplot(gs[3, :])

ax5.axis("off")

ax5.text(
    0.5,
    0.85,
    "KEY INSIGHTS",
    ha="center",
    fontsize=18,
    fontweight="bold"
)

ax5.text(
    0.5,
    0.56,
    f"• The dataset contains {total_books} books across {total_genres} different genres.",
    ha="center",
    fontsize=12
)

ax5.text(
    0.5,
    0.32,
    f"• The average rating of all books is {average_rating:.2f}.",
    ha="center",
    fontsize=12
)

ax5.text(
    0.5,
    0.08,
    f"• {most_common_genre} is the most common genre with {most_common_genre_count} books.",
    ha="center",
    fontsize=12
)



# 11. SAVE DASHBOARD


plt.savefig(
    "library_dashboard.png",
    dpi=300,
    bbox_inches="tight"
)



# 12. DISPLAY DASHBOARD


plt.show()


print("\n" + "=" * 60)
print("LIBRARY BOOK DATA ANALYZER")
print("=" * 60)

print(f"Total Books       : {total_books}")
print(f"Average Rating    : {average_rating:.2f}")
print(f"Total Genres      : {total_genres}")
print(f"Total Authors     : {total_authors}")

print("\nMost Common Genre")
print("-" * 60)
print(
    f"{most_common_genre} with {most_common_genre_count} books"
)

print("\nHighest Rating")
print("-" * 60)
print(f"Rating : {highest_rating}")
print(f"Book   : {highest_rated_book}")

print("\nDashboard created successfully!")
print("File: library_dashboard.png")
print("=" * 60)
