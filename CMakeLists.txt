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
                        main/abstract_algebra/abstract_algebra.tex
                        main/abstract_algebra/algebraic_structures.tex
                        main/abstract_algebra/algebras.tex
                        main/abstract_algebra/bilinear_operations.tex
                        main/abstract_algebra/functions.tex
                        main/abstract_algebra/morphisms.tex
                        main/abstract_algebra/representation_theory.tex
                        main/linear_algebra/commutators.tex
                        main/linear_algebra/fields.tex
                        main/linear_algebra/linear_algebra.tex
                        main/linear_algebra/matrix.tex
                        main/linear_algebra/symmetric_eigenvalue_problem.tex
                        main/linear_algebra/systems_of_equations.tex
						appendices/proofs.tex
					IMAGE_DIRS
						images
					)


# POST-BUILD: move the created .pdf-file to the top directory (copy and delete)
add_custom_command(TARGET "${TEX_NAME}_pdf" POST_BUILD
COMMAND ${CMAKE_COMMAND} -E copy "${TEX_NAME}.pdf" ..
COMMAND ${CMAKE_COMMAND} -E remove "${TEX_NAME}.pdf"
COMMENT "Moving PDF-file to top directory.")
