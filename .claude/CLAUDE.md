# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Context

This is a data analysis project for Tesa's General Industry business unit. Tesa is a global adhesive solutions manufacturer specializing in industrial adhesive tapes for automotive, electronics, renewable energy, and manufacturing sectors.

For detailed company context, see [.claude/notes/context.md](.claude/notes/context.md).

## Environment Setup

This project uses Conda for environment management with Python 3.14.

### Create and activate environment:
```sh
conda env create -f environment.yml
conda activate tesa
```

### Update environment after modifying environment.yml:
```sh
conda env update -f environment.yml
```

## Dependencies

The project includes the following Python packages:
- **pandas**: Data manipulation and analysis
- **ipython**: Interactive Python shell
- **python-pptx**: PowerPoint presentation generation
- **openpyxl**: Excel file reading and writing

## Project Structure

This is an early-stage project currently being set up. Code and data analysis files will be added as the project develops.
