cmake_minimum_required(VERSION 3.9)

# Specify the tex file name
set(TEX_NAME mathematics)

# Define a LaTeX project, and specify where to find the UseLATEX commands
project(mathematics NONE)  # the NONE option has to be included, since we are not using the langue c, cxx, or Fortran
include(cmake/UseLATEX.cmake)  # I like anti-cluttering by moving the UseLATEX.cmake file into a separate directory


# BUILD: Add a file to the specified project
add_latex_document(${TEX_NAME}.tex BIBFILES ../../../../../Archief/Bibliotheek/research_bib.bib
                   INPUTS
                        config/commands.tex
                        config/packages.tex
                        main/algebraic_structures.tex
                        main/algebras.tex
                        main/bilinear_operations.tex
                        main/commutators.tex
                        main/fields.tex
                        main/functions.tex
                        main/matrix.tex
                        main/morphisms.tex
                        main/representation_theory.tex
                        main/symmetric_eigenvalue_problem.tex
                        main/systems_of_equations.tex
						appendices/proofs.tex
					IMAGE_DIRS
						images
					)


# POST-BUILD: move the created .pdf-file to the top directory (copy and delete)
add_custom_command(TARGET "${TEX_NAME}_pdf" POST_BUILD
COMMAND ${CMAKE_COMMAND} -E copy "${TEX_NAME}.pdf" ..
COMMAND ${CMAKE_COMMAND} -E remove "${TEX_NAME}.pdf"
COMMENT "Moving PDF-file to top directory.")
